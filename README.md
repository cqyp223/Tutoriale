**⚠️ Uwaga:** [Zapoznaj się przed skorzystaniem z niniejszego repozytorium!](DISCLAIMER.md)


# Spis treści:
1. [Tutotial Git](Git/git_gpt.md)
2. [Tutotial Git - Wersjonowanie programów w Git](Git/git_wersje_gpt.md)
3. [Markdown – praktyczny tutorial](Markdown/Markdown-tutorial.md)


# Sposoby generowania plików, w formacie, PDF oraz EPUB

## Instalacja wymaganych programów

Aby móc skonwertować pliki w formacie Markdown na format PDF lub EPUB należy zainstalować poniższe programy (dla Debiana i systemów debianopodobnych):

```bash
sudo apt update
sudo apt install pandoc texlive-xetex texlive-fonts-recommended
```

## Konwersja do PDF:

```bash
pandoc twoj_plik.md -o gotowy_plik.pdf --pdf-engine=xelatex -V geometry:a5paper
```

Jeśli chcemy np. zmniejszyć marginesy:

```bash
pandoc twoj_plik.md -o gotowy_plik.pdf --pdf-engine=xelatex -V geometry:"a5paper, margin=1.5cm"
```

## Konwersja do EPUB:

```bash
pandoc twoj_plik.md -o gotowy_plik.epub
```

Jeśli chcemy dodać tytuł i autora - lepiej się prezentuje na czytnikach e-book'ów:

```bash
pandoc twoj_plik.md -o gotowy_plik.epub --toc --metadata title="Tytuł Książki" --metadata author="Imię i Nazwisko"
```

Możemy jeszcze dodać okłądkę:

```bash
pandoc twoj_plik.md -o gotowy_plik.epub --toc --epub-cover-image=okladka.jpg --metadata title="Tytuł Książki" --metadata author="Imię i Nazwisko"
```

