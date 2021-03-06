#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2015 Toomas Soome <tsoome@me.com>
# Copyright 2016 RackTop Systems.
#

include $(SRC)/Makefile.master

CC=     $(GCC_ROOT)/bin/gcc

LIB=	efi

all:	lib$(LIB).a

install:

SRCS=	delay.c efi_console.c efinet.c efipart.c errno.c handles.c \
	libefi.c time.c

OBJS=	$(SRCS:%.c=%.o)

CPPFLAGS= -DTERM_EMU
CFLAGS = -O2

#.if ${MACHINE_CPUARCH} == "aarch64"
#CFLAGS+=	-msoft-float -mgeneral-regs-only
#.endif
#.if ${MACHINE_ARCH} == "amd64"
CFLAGS += -fPIC
#.endif

CFLAGS += -nostdinc -I. -I../../../../include -I../../..
CFLAGS += -I../include
CFLAGS += -I../include/${MACH64}
CFLAGS += -I../../../../lib/libstand

# Pick up the bootstrap header for some interface items
CFLAGS += -I../../common

# Handle FreeBSD specific %b and %D printf format specifiers
# CFLAGS+= ${FORMAT_EXTENSIONS}
# CFLAGS += -D__printf__=__freebsd_kprintf__
CFLAGS+= -DTERM_EMU

include ../Makefile.inc

lib$(LIB).a: $(SRCS) $(OBJS)
	$(AR) $(ARFLAGS) $@ $(OBJS)

clean: clobber
clobber:
	$(RM) $(CLEANFILES) $(OBJS) machine x86 lib$(LIB).a

machine:
	$(RM) machine
	$(SYMLINK) ../../../amd64/include machine

x86:
	$(RM) x86
	$(SYMLINK) ../../../x86/include x86

$(OBJS): machine x86
