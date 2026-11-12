# **FFMPEG** - sprzętowa konwersja video

## Zapobieganie zielonym i/lub czarnym pasom po sprzętowej konversji vodeo enkoderami kart graficznych kart AMD Radeon

### "Wstrzyknięcie" informacji o przycięciu bezpośrednio do nagłówków SPS

To absolutnie najlepsze i najbezpieczniejsze podejście. Wstrzyknięcie informacji o przycięciu (tzw. Conformance Window lub Default Display Window) bezpośrednio do nagłówków SPS (Sequence Parameter Set) w surowym strumieniu H.265 - i nie tylko - gwarantuje, że odtwarzacz nie ma prawa ich zignorować. O ile metadane kontenera MKV bywają pomijane przez niektóre smart TV czy proste dekodery sprzętowe, o tyle każdy dekoder musi przetworzyć nagłówki SPS strumienia, aby w ogóle rozpocząć wyświetlanie jakichkolwiek klatek.

Służy do tego potężny mechanizm Bitstream Filters (BSF) w FFmpeg. Filtr hevc_metadata modyfikuje wyłącznie bity informacyjne samego strumienia, nie dekodując ani nie uszkadzając właściwych makrobloków obrazu.

#### Można to wdrożyć na dwa sposoby:
1. Modyfikacja bitstreamu w gotowym pliku (bez rekompresji)

Jeśli masz już plik 1920x1088 z wygenerowanym przez Radeona zielonym paskiem, wystarczy skopiować wszystkie strumienie i zastosować filtr BSF na ścieżce wideo:

```bash
ffmpeg -i wejscie.mkv -c copy -bsf:v hevc_metadata=crop_bottom=8 wyjscie.mkv
```

*Weryfikacja:* Polecenie wykonuje się błyskawicznie (z prędkością dysku), ponieważ to tylko kopiowanie z łatą nagłówka. Obraz w pliku wyjscie.mkv zachowa fizycznie 1088 pikseli w pionie, ale każdy sprzętowy odtwarzacz natywnie przytnie dolne 8 pikseli przed wyświetleniem obrazu na ekranie.

2. Wstrzyknięcie w locie podczas kodowania sprzętowego (Zalecane)

Dla pełnej automatyzacji w Twoich skryptach Bash, najwygodniej jest dokleić BSF prosto do łańcucha kodującego VA-API. Procesor VCN na RX 7600 zakoduje surowe, sprzętowe 1088 linii ze wszystkimi artefaktami na marginesie, ale FFmpeg "wstrzyknie" łatkę ukrywającą dół, zanim włoży gotowy obraz do kontenera.

```bash
ffmpeg -hwaccel vaapi -hwaccel_device /dev/dri/renderD128 -hwaccel_output_format vaapi \
-i wejscie.mp4 \
-c:v hevc_vaapi -b:v 5M \
-bsf:v hevc_metadata=crop_bottom=8:crop_right=8 \
wyjscie.mkv
```

*Wskazówka:* upewnij się, że /dev/dri/renderD128 wskazuje u Ciebie na urządzenie AMD – w systemach z wieloma układami, takimi jak RX 7600 w parze z procesorem wyposażonym w zintegrowany Intel UHD 630, Radeon często widnieje pod węzłem renderD129).

#### Dlaczego ta metoda deklasuje obcinanie na poziomie MKV?
- Pełna przenośność: Plik zakodowany w ten sposób można swobodnie wyciągać z MKV, przepakowywać do MP4 czy surowego strumienia .265 – metadane obcięcia zawsze będą podróżować razem z samym obrazem, ponieważ są wpisane w jego nierozerwalną strukturę.

- Zgodność przestrzeni kolorów: Filtr hevc_metadata edytuje oficjalne pola specyfikacji VUI (Video Usability Information). Ze względu na rygorystyczne zasady standardu H.265 dla najpopularniejszej przestrzeni kolorów 4:2:0, przycinanie musi odbywać się co 2 piksele. Ucięcie równej wartości 8 idealnie spełnia ten techniczny wymóg, eliminując ryzyko odrzucenia pliku przez rygorystyczne parsery.

**⚠️ Złota zasada parzystości (Format 4:2:0)**
Wartości przycięcia dla kodeka HEVC muszą być liczbami parzystymi (podzielnymi przez 2). Standardowy obraz z Radeona używa próbkowania kolorów 4:2:0, co oznacza, że warstwa kolorów (chroma) ma o połowę mniejszą rozdzielczość niż warstwa jasności (luma). Użycie nieparzystej wartości (np. crop_right=7) spowoduje, że dekoder nie będzie w stanie poprawnie nałożyć mapy kolorów na krawędzie, co w skrajnych przypadkach może doprowadzić do błędu dekodowania lub "rozjechania" barw.

#### Kiedy encoder sprzętowy wyrównuje do 16, kiedy do 32, a kiedy do 64 pixeli?

To, jakiego wyrównania (paddingu) użyje sprzętowy koder wideo, zależy od wybranego standardu kompresji (kodeka) oraz architektury samego procesora graficznego. Różne kodeki opierają się na blokach danych o innych rozmiarach.

#####Oto jak koder dobiera wyrównanie:

- Wyrównanie do 16 pikseli (MOD16) — H.264 (AVC)
Starszy standard H.264 działa na rygorystycznej siatce tzw. makrobloków (Macroblocks). Każdy makroblok ma stały rozmiar 16x16 pikseli. Wymusza to na każdym koderze sprzętowym (niezależnie czy to AMD, Intel, czy Nvidia) fizyczne podzielenie bufora obrazu na wielokrotności liczby 16. Jest to absolutne minimum w nowoczesnym wideo.

- Wyrównanie do 32 lub 64 pikseli (MOD32 / MOD64) — HEVC (H.265)
Kodek HEVC zrezygnował ze sztywnych makrobloków na rzecz CTU?. Koder może dynamicznie decydować o ich rozmiarze (od 16x16 do 64x64 pikseli). W sprzętowej implementacji AMD VCN dla HEVC, procesor często wyrównuje bufory pamięci VRAM do wielokrotności 32 pikseli (dlatego 1080p jest rozszerzane do 1088, ponieważ 1088 dzieli się przez 32), aby zoptymalizować transfer danych na szynie pamięci. Przy rozdzielczościach 4K (UHD) sprzęt może przełączyć się na wymuszony grid 64x64.

- Wyrównanie do 64 lub 128 pikseli (MOD64 / MOD128) — AV1
Najnowszy otwarty standard AV1 wprowadził tzw. Superblocks?. Aby osiągnąć maksymalny stopień kompresji przy wysokich rozdzielczościach, układy sprzętowe kodujące do AV1 (w tym silniki VCN 4.0 z serii RX 7000) rezerwują w pamięci obszary w wielokrotnościach 64, a dla materiałów 8K nawet 128 pikseli.

Z punktu widzenia automatyzacji w skryptach Bash, najbezpieczniej jest zawsze wyrównywać materiały HEVC i AV1 do wielokrotności 32 pikseli za pomocą filtrów, co w 100% zaspokaja wymogi kontrolerów pamięci Intela i AMD, unikając powstawania nieprzewidzianych marginesów.

