# $Id: Makefile.in,v 1.59.2.15 2005/02/22 03:02:40 jnelson Exp $

.SUFFIXES:
.SUFFIXES: .o .c
.PHONY: clean mrclean distclean all dist depend

# The following gcc warning switches are too noisy to be useful checking
# Boa for lint:
#  -Wtraditional -Wconversion -Wredundant-decls -Wunreachable-code
# The following gcc warning switches should generate no warnings:
GCC_FLAGS = -Wstrict-prototypes -Wpointer-arith -Wcast-align -Wcast-qual \
  -Wshadow -Waggregate-return -Wmissing-prototypes -Wnested-externs \
  -Wall -W -Wno-unused -Winline -Wwrite-strings -Wundef -pedantic

srcdir = .
VPATH = ./../extras
LDFLAGS =  -g
LIBS = 
CFLAGS = -Os -I/home/wig/workspace/nuts/rt1050/buildroot/output/host/rm-buildroot-uclinux-uclibcgnueabi/sysroot/usr/include -pipe -Wall
CPPFLAGS =  -I. -I.
DEPEND = .depend
BUILD_DIR = $(CURDIR)/../output

CC = /home/wig/workspace/nuts/rt1050/buildroot/output/host/usr/bin/arm-buildroot-uclinux-uclibcgnueabi-gcc 
CPP = /home/wig/workspace/nuts/rt1050/buildroot/output/host/usr/bin/arm-buildroot-uclinux-uclibcgnueabi-gcc -E

SOURCES = alias.c auth.c boa.c buffer.c cgi.c cgi_header.c config.c escape.c \
	get.c hash.c ip.c log.c md5.c mmap_cache.c pipe.c queue.c range.c \
	read.c request.c response.c signals.c util.c sublog.c \
	select.c 

OBJS = $(SOURCES:.c=.o) timestamp.o 

all:	boa boa_indexer

boa:	$(OBJS) 
	$(CC) -o $@ $^ $(LDFLAGS) $(LIBS)
	mv boa $(BUILD_DIR)
	
boa_indexer:	index_dir.o escape.o   
	$(CC) -o $@ $^ $(LDFLAGS) $(LIBS)
	mv boa_indexer $(BUILD_DIR)

clean:
	rm -f $(OBJS) boa core *~ boa_indexer index_dir.o
	rm -f    poll.o select.o access.o
	
distclean:	mrclean

mrclean:	clean
	rm -f config.status config.cache config.h Makefile config.log

# timestamp

timestamp.o:	$(SOURCES)

# depend stuff
depend: $(SOURCES)
	$(CPP) $(CPPFLAGS) -MM $^ select.c poll.c access.c > $(DEPEND)
        
-include $(DEPEND)


# tags
tags:	$(SOURCES)
	ctags -o tags $^ *.h

# object dump
boa.objdump:    boa
	objdump --disassemble-all --source boa > $@

