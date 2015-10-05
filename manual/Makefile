BOOK=	"UNIX for Kids"

SRCS=	intro.1 man.1 sh.1						\
	at.1 bc.1 cp.1 date.1 echo.1 find.1 grep.1 head.1 id.1 jot.1	\
	kill.1 ls.1 more.1 nc.1 od.1 ps.1 quota.1 rm.1 sort.1 tail.1	\
	uniq.1 vi.1 wc.1 xargs.1 yes.1 zcat.1				\
	hier.7 glob.7 re_format.7

OBJS=	${SRCS:M*.1:S/$/.ps/}
OBJS+=	${SRCS:M*.7:S/$/.ps/}

PGSIZE=	a5
GSOPTS=	-q -dSAFER -dBATCH -dNOPAUSE -dPDFSETTINGS=/prepress
GSOPTS+=-sDEVICE=pdfwrite -sPAPERSIZE=${PGSIZE}

all: book

book: ps ${OBJS}
	gs ${GSOPTS} -sOutputFile="UNIX_for_Kids.pdf" ${OBJS}

ps: ${SRCS}
.for x in ${SRCS}
	mandoc -Opaper=${PGSIZE} -Tps -Ios=${BOOK} ${.CURDIR}/${x} > ${x}.ps
.endfor
	perl -pi -e 's/ZZZZZZZZ/"Page ".++$$n/ge' ${OBJS}

lint: ${SRCS}
.for x in ${SRCS}
	mandoc -Tlint ${.CURDIR}/${x}
.endfor

clean:
	rm *.ps *.pdf
