TEXFILES=$(shell find . -name "*.tex")
BIBFILES=$(shell find . -name "*.bib")
TEXOPTS=--interaction nonstopmode --output-directory out --file-line-error

MAINFILE=cv

all: out/$(MAINFILE).pdf

out:
	mkdir -p out

out/$(MAINFILE).pdf: $(TEXFILES) $(BIBFILES) out
	pdflatex $(TEXOPTS) $(MAINFILE).tex
	bibtex out/art.aux
	bibtex out/conf.aux
	bibtex out/post.aux
	bibtex out/tr.aux
	pdflatex $(TEXOPTS) $(MAINFILE).tex
	pdflatex $(TEXOPTS) $(MAINFILE).tex | cat
	cat out/$(MAINFILE).log | sed -e "s/^/-->/" | grep ".*:[0-9]*:.*" ; \
	  if [ $$? = "0" ]; then echo "ERRORS FOUND!"; false; else true; fi

clean:
	rm -rf out
