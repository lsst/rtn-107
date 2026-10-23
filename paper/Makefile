DOCNAME = mdc_paper

GITVERSION := $(shell git log -1 --date=short --pretty=%h)
GITDATE := $(shell git log -1 --date=short --pretty=%ad)
GITSTATUS := $(shell git status --porcelain -- .)
ifneq "$(GITSTATUS)" ""
	GITDIRTY = -dirty
endif

# lsst-texmf is the git submodule at the repository root
export TEXMFHOME = ../lsst-texmf/texmf

$(DOCNAME).pdf: $(DOCNAME).tex references.bib meta.tex
	latexmk -bibtex -xelatex -f $(DOCNAME)

# meta.tex is generated (and gitignored)
meta.tex: $(DOCNAME).tex
	printf '%% GENERATED FILE -- edit this in the Makefile\n\\newcommand{\\lsstDocType}{RTN}\n\\newcommand{\\lsstDocNum}{107}\n\\newcommand{\\vcsRevision}{$(GITVERSION)$(GITDIRTY)}\n\\newcommand{\\vcsDate}{$(GITDATE)}\n' > meta.tex

.PHONY: clean
clean:
	latexmk -c
	rm -f $(DOCNAME).{bbl,pdf}
	rm -f meta.tex
