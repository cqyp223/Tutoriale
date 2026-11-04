sudo apt update
sudo apt install pandoc texlive-xetex texlive-fonts-recommended


PDF:

pandoc twoj_plik.md -o gotowy_plik.pdf --pdf-engine=xelatex -V geometry:a5paper

pandoc twoj_plik.md -o gotowy_plik.pdf --pdf-engine=xelatex -V geometry:"a5paper, margin=1.5cm"



EPUB:

pandoc twoj_plik.md -o gotowy_plik.epub

pandoc git_gpt.md -o git_gpt.epub --toc --metadata title="Git Tutorial" --metadata author="Chat GPT"

pandoc git_gpt.md -o git_gpt.epub --toc --epub-cover-image=okladka.jpg --metadata title="Tytuł Książki" --metadata author="Imię i Nazwisko"

