PREFIX := .
SOURCE_DIR := ${PREFIX}/src
PUBLIC_DIR := ${PREFIX}/public
HTML_DIR := ${PREFIX}/html

FILENAME := twjrtemplate
TWJR_FILENAME := ${FILENAME}.twjr
TEXI_FILENAME := ${FILENAME}.texi
INFO_FILENAME := ${FILENAME}.info
PDF_FILENAME  := ${FILENAME}.pdf

.Phony : all
all : tangle weave

.Phony : tangle
tangle :
	jrtangle ${TWJR_FILENAME}

.Phony : weave
weave : ${TEXI_FILENAME}

${TEXI_FILENAME} : ${TWJR_FILENAME}
	jrweave ${TWJR_FILENAME} > ${TEXI_FILENAME}

.Phony : info
info : ${INFO_FILENAME}

${INFO_FILENAME} : ${TEXI_FILENAME}
	makeinfo ${TEXI_FILENAME}

.Phony : pdf
pdf : ${PDF_FILENAME}

${PDF_FILENAME} : ${TEXI_FILENAME}
	pdftexi2dvi ${TEXI_FILENAME}

.Phony : pdf-open
pdf-open : ${PDF_FILENAME}
	open ${PDF_FILENAME}

.Phony : clean
clean :
	rm -f *~
	rm -f *.??
	rm -r *.{aux,cps,log,toc}

.Phony : dist-clean
dist-clean : clean
	rm -f *.texi
	rm -f *.info

.Phony : ${SOURCE_DIR}
${SOURCE_DIR} :
	mkdir -p ${SOURCE_DIR}

.Phony : ${PUBLIC_DIR}
${PUBLIC_DIR} :
	mkdir -p ${PUBLIC_DIR}

.Phony : ${HTML_DIR}
${HTML_DIR} :
	mkdir -p ${HTML_DIR}


.Phony : move-js-to-source
move-js-to-source : | ${SOURCE_DIR}
	find ${PREFIX} -depth=1 -name \*.js -exec mv {} ${SOURCE_DIR} \;

.Phony : move-html
move-html : | ${HTML_DIR}
	find ${PREFIX} -depth=1 -name \*.html -exec mv {} ${HTML_DIR}\;

