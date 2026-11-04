# Markdown – praktyczny tutorial

## 1. Czym jest Markdown?

Markdown to lekki język znaczników służący do formatowania tekstu za pomocą prostych znaków specjalnych.

Pliki Markdown mają najczęściej rozszerzenie:
- `.md`
- `.markdown`

Zwykły plik tekstowy zapisany w Markdown można otworzyć w dowolnym edytorze tekstowym, np. gedit, Notatniku czy Vimie.

Przykładowo:

```markdown
# Mój dokument

To jest zwykły tekst.

**Ten tekst jest pogrubiony.**
```

Po wyrenderowaniu dokumentu otrzymamy nagłówek, zwykły akapit i pogrubiony tekst.

## 2. Nagłówki

Nagłówki tworzy się za pomocą znaku `#`.

Im więcej znaków `#`, tym niższy poziom nagłówka.

```markdown
# Nagłówek poziomu 1

## Nagłówek poziomu 2

### Nagłówek poziomu 3

#### Nagłówek poziomu 4

##### Nagłówek poziomu 5

###### Nagłówek poziomu 6
```

Nagłówek poziomu 1 jest odpowiednikiem głównego tytułu dokumentu.

**Uwaga:** po znakach `#` należy wstawić spację.

## 3. Akapity i łamanie linii

Zwykły tekst nie wymaga żadnych dodatkowych oznaczeń.

```markdown
To jest pierwszy akapit.

To jest drugi akapit.
```

Pusta linia oddziela akapity.

Jeżeli chcemy wymusić przejście do nowej linii bez rozpoczynania nowego akapitu, możemy użyć dwóch spacji na końcu wiersza albo znacznika `<br>`.

```markdown
Pierwsza linia.  
Druga linia.
```

## 4. Formatowanie tekstu

| Zapis Markdown | Efekt |
|---|---|
| `**tekst**` | **Pogrubienie** |
| `*tekst*` | *Kursywa* |
| `***tekst***` | ***Pogrubiona kursywa*** |
| `~~tekst~~` | ~~Przekreślenie~~ |
| `` `tekst` `` | `Kod w tekście` |

Przykład:

```markdown
To jest **ważna informacja**.

To jest *wyróżnienie*.

To jest ~~nieaktualna informacja~~.

Polecenie `ls -la` wyświetla zawartość katalogu.
```

## 5. Listy punktowane

Listę punktowaną można utworzyć za pomocą `-`, `*` lub `+`.

```markdown
- Pierwszy element
- Drugi element
- Trzeci element
```

Można również tworzyć listy zagnieżdżone:

```markdown
- System Linux
  - Debian
  - Ubuntu
  - Fedora
- System Windows
  - Windows 10
  - Windows 11
```

Wcięcie określa poziom zagnieżdżenia.

## 6. Listy numerowane

Listę numerowaną tworzy się za pomocą liczby i kropki.

```markdown
1. Pierwszy krok
2. Drugi krok
3. Trzeci krok
```

Listy można zagnieżdżać:

```markdown
1. Instalacja systemu
   1. Przygotowanie nośnika
   2. Uruchomienie instalatora
2. Konfiguracja
   1. Ustawienie sieci
   2. Instalacja pakietów
```

Markdown automatycznie numeruje elementy listy w wielu rendererach, dlatego można również używać `1.` przy każdym elemencie.

## 7. Listy z polami wyboru

Popularne rozszerzenie Markdown obsługuje listy kontrolne.

```markdown
- [ ] Instalacja systemu
- [ ] Konfiguracja sieci
- [x] Aktualizacja pakietów
- [ ] Instalacja dodatkowego oprogramowania
```

Wynik:

- [ ] Instalacja systemu
- [ ] Konfiguracja sieci
- [x] Aktualizacja pakietów
- [ ] Instalacja dodatkowego oprogramowania

`[ ]` oznacza zadanie niewykonane, a `[x]` – wykonane.

## 8. Bloki kodu

Kod można umieszczać pomiędzy trzema znakami odwrotnego apostrofu (backtick):

````markdown
```
Tutaj znajduje się kod.
```
````

Można również określić język programowania. Dzięki temu edytor lub przeglądarka Markdown może zastosować kolorowanie składni.

Przykład:

````markdown
```python
#!/usr/bin/env python3

print("Hello World!")
```
````

Przykład dla Bash:

````markdown
```bash
#!/bin/bash

echo "Hello World!"
```
````

Przykład dla C:

````markdown
```c
#include <stdio.h>

int main(void)
{
    printf("Hello World!\n");
    return 0;
}
```
````

## 9. Cytaty

Cytat rozpoczyna się od znaku `>`.

```markdown
> To jest cytat.
>
> Może składać się z kilku akapitów.
```

Możliwe jest również zagnieżdżanie cytatów:

```markdown
> Pierwszy poziom cytatu.
>
> > Drugi poziom cytatu.
```

## 10. Linie poziome

Trzy lub więcej myślników, gwiazdek albo podkreśleń tworzą poziomą linię.

```markdown
---
```

Można jej używać do oddzielania sekcji dokumentu.

## 11. Linki

Link do strony internetowej zapisuje się w następujący sposób:

```markdown
[Google](https://www.google.com)
```

Tekst w nawiasach kwadratowych jest wyświetlaną nazwą odnośnika, a adres w nawiasach okrągłych jest jego celem.

Przykład:

```markdown
Dokumentacja systemu znajduje się na stronie
[Debian](https://www.debian.org/).
```

Można również dodać opis wyświetlany po najechaniu kursorem:

```markdown
[Debian](https://www.debian.org/ "Oficjalna strona Debiana")
```

## 12. Obrazy

Obraz wstawia się podobnie jak link, ale z wykrzyknikiem na początku.

```markdown
![Opis obrazu](images/obraz.png)
```

Można używać adresów internetowych:

```markdown
![Logo](https://example.com/logo.png)
```

Opis w nawiasach kwadratowych jest tekstem alternatywnym, wyświetlanym np. wtedy, gdy obraz nie może zostać załadowany.

## 13. Tabele

Tabele tworzy się za pomocą pionowych kresek `|` oraz myślników.

```markdown
| Nazwa | System | Wersja |
|-------|--------|--------|
| Debian | Linux | 13 |
| Ubuntu | Linux | 26.04 |
| Windows | Microsoft | 11 |
```

Wynik:

| Nazwa | System | Wersja |
|---|---|---|
| Debian | Linux | 13 |
| Ubuntu | Linux | 26.04 |
| Windows | Microsoft | 11 |

Można również ustawić wyrównanie zawartości kolumn:

```markdown
| Lewa | Środek | Prawa |
|:-----|:------:|------:|
| A | B | C |
| 10 | 20 | 30 |
```

- `:---` – wyrównanie do lewej.
- `:---:` – wyśrodkowanie.
- `---:` – wyrównanie do prawej.

## 14. Znaki specjalne

Niektóre znaki mają w Markdown specjalne znaczenie. Aby wyświetlić je dosłownie, należy poprzedzić je odwrotnym ukośnikiem `\`.

Przykłady:

```markdown
\* To nie jest kursywa.

\# To nie jest nagłówek.

\[tekst\](adres) – zapis bez tworzenia linku.
```

Najczęściej używane znaki wymagające poprzedzenia ukośnikiem:

```text
\ ` * _ { } [ ] ( ) # + - . ! |
```

## 15. Odsyłacze do innych miejsc w dokumencie

Można tworzyć linki prowadzące do nagłówków w tym samym dokumencie.

Przykład:

```markdown
## Instalacja

Opis instalacji...

## Konfiguracja

[Przejdź do instalacji](#instalacja)
```

Identyfikator odsyłacza jest zazwyczaj tworzony na podstawie tekstu nagłówka: małe litery, spacje zamienione na myślniki, bez większości znaków specjalnych.

## 16. Przypisy

Przypisy są obsługiwane przez wiele popularnych implementacji Markdown, np. rozszerzenia używane przez Pandoc i GitHub.

```markdown
Markdown jest lekkim językiem znaczników.[^1]

[^1]: Więcej informacji: https://www.markdownguide.org/
```

Nie każdy renderer Markdown obsługuje przypisy.

## 17. Komentarze HTML

Komentarze HTML nie są wyświetlane w wyrenderowanym dokumencie.

```markdown
<!-- To jest komentarz. -->

# Dokumentacja

<!-- Tutaj można umieścić własne uwagi. -->
```

To przydatne np. do zapisywania notatek dla autora dokumentu.

## 18. Metadane YAML (Front Matter)

Niektóre systemy, np. generatory stron statycznych, obsługują blok metadanych umieszczony na początku pliku.

```yaml
---
title: "Dokumentacja projektu"
author: "Łukasz Marcińczak"
date: 2026-11-02
version: 1.0.0
---
```

Taki blok nazywa się *YAML Front Matter*. Nie jest częścią podstawowego standardu Markdown – jego obsługa zależy od używanego narzędzia.

## 19. Przykładowy kompletny dokument

Poniżej znajduje się przykładowy dokument łączący większość poznanych elementów.

````markdown
# Instalacja i konfiguracja programu

**Wersja:** 1.0.0  
**Data:** 2026-11-02  
**Autor:** Łukasz Marcińczak

## 1. Wymagania

Do instalacji potrzebne są:

- System Debian 13.
- Dostęp do Internetu.
- Uprawnienia administratora.

## 2. Instalacja

Wykonaj polecenie:

```bash
sudo apt update
sudo apt install program
```

## 3. Konfiguracja

Plik konfiguracyjny znajduje się w katalogu:

`/etc/program/`

Przykładowa konfiguracja:

```ini
[general]
enabled=true
port=8080
```

## 4. Lista kontrolna

- [x] Instalacja pakietu
- [ ] Konfiguracja programu
- [ ] Test działania

## 5. Przydatne informacje

Dokumentacja: [Oficjalna strona](https://example.com/)

> Pamiętaj o wykonaniu kopii zapasowej pliku konfiguracyjnego.

---

*Koniec dokumentu.*
````

## 20. Czym różnią się Markdown i jego odmiany?

Markdown nie jest jednym, całkowicie jednolitym formatem. Istnieją różne implementacje i rozszerzenia.

| Odmiana | Charakterystyka |
|---|---|
| CommonMark | Ujednolicona specyfikacja podstawowej składni Markdown |
| GitHub Flavored Markdown (GFM) | Rozszerzenia używane m.in. przez GitHub |
| MultiMarkdown | Dodatkowe możliwości, m.in. przypisy i metadane |
| Pandoc Markdown | Rozbudowana składnia używana przez Pandoc |

W praktyce najczęściej spotyka się składnię CommonMark oraz GitHub Flavored Markdown.

## 21. Przydatne narzędzia

- **gedit** – edycja zwykłych plików `.md`.
- **Vim** – edycja Markdown w terminalu.
- **Visual Studio Code** – edycja z podglądem Markdown.
- **GitHub** – automatyczne wyświetlanie plików Markdown w repozytoriach.
- **Pandoc** – konwersja Markdown do HTML, PDF, DOCX i innych formatów.

Przykładowa konwersja za pomocą Pandoc:

```bash
pandoc dokument.md -o dokument.html
pandoc dokument.md -o dokument.docx
pandoc dokument.md -o dokument.pdf
```

Konwersja do PDF może wymagać dodatkowego silnika PDF, np. LaTeX.

## 22. Podsumowanie

Najważniejsze elementy składni Markdown:

| Element | Składnia |
|---|---|
| Nagłówek | `# Nagłówek` |
| Pogrubienie | `**tekst**` |
| Kursywa | `*tekst*` |
| Przekreślenie | `~~tekst~~` |
| Lista punktowana | `- element` |
| Lista numerowana | `1. element` |
| Kod w tekście | `` `kod` `` |
| Blok kodu | ` ```język ... ``` ` |
| Cytat | `> cytat` |
| Link | `[tekst](adres)` |
| Obraz | `![opis](plik)` |
| Tabela | `| kolumna | kolumna |` |
| Linia pozioma | `---` |
| Komentarz | `<!-- tekst -->` |

**Najważniejsza zaleta Markdown:** dokument jest zwykłym tekstem, czytelnym nawet bez specjalnego programu, a jednocześnie można go łatwo przekształcić w estetyczny dokument HTML, PDF lub DOCX.

