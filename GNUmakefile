
FIND= find
PNAME=template

all: ${PNAME}.tex ${PNAME}.pdf

EPS_FILES = $(shell ${FIND} ./ -name *.eps 2>/dev/null)
PDF_TARGETS = $(addsuffix .pdf, $(basename $(notdir $(EPS_FILES))))

${PNAME}.tex:
	env TMPDIR=./  pod6slide  ${PNAME}.pod6 >$@
${PNAME}.pdf: ${PNAME}.tex $(PDF_TARGETS)
	pdflatex -halt-on-error ${PNAME}.tex; touch $@

$(PDF_TARGETS): BASE = $(basename $(notdir $@))
$(PDF_TARGETS): ORIG = $(filter %/${BASE}.eps,${EPS_FILES})
$(PDF_TARGETS):
	echo CONVERT ${ORIG} to $@;\
	epstopdf ${ORIG}  -o=$@
	
clean:
	-rm -df *.tmp *.tex *.pdf *.log *.snm *.aux *.nav *.out *.toc *.dvi *.vrb

