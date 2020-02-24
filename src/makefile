#/***********************************************************************************
#    Copyright 2006 Charles F. Gammie, Jonathan C. McKinney, Scott C. Noble, 
#                   Gabor Toth, and Luca Del Zanna
#
#                        HARM  version 1.0   (released May 1, 2006)
#
#    This file is part of HARM.  HARM is a program that solves hyperbolic 
#    partial differential equations in conservative form using high-resolution
#    shock-capturing techniques.  This version of HARM has been configured to 
#    solve the relativistic magnetohydrodynamic equations of motion on a 
#    stationary black hole spacetime in Kerr-Schild coordinates to evolve
#    an accretion disk model. 
#
#    You are morally obligated to cite the following two papers in his/her 
#    scientific literature that results from use of any part of HARM:
#
#    [1] Gammie, C. F., McKinney, J. C., \& Toth, G.\ 2003, 
#        Astrophysical Journal, 589, 444.
#
#    [2] Noble, S. C., Gammie, C. F., McKinney, J. C., \& Del Zanna, L. \ 2006, 
#        Astrophysical Journal, 641, 626.
#
#   
#    Further, we strongly encourage you to obtain the latest version of 
#    HARM directly from our distribution website:
#    http://rainman.astro.uiuc.edu/codelib/
#
#
#    HARM is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    HARM is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with HARM; if not, write to the Free Software
#    Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
#
#***********************************************************************************/
#### set USEICC to 0 if you want gcc compiler options, else set to 1 to use icc
########  gcc generally used for debugging with -g option so we can use gdb 
USEICC = 1


ifeq ($(USEICC),1)
CC       = icc
CCFLAGS  = -O3 -axW -tpp7
#CCFLAGS  = -O2
endif

ifeq ($(USEICC),0)
CC       = gcc
CCFLAGS  = -g
endif


EXTRALIBS = -lm

CC_COMPILE  = $(CC) $(CCFLAGS) -c 
CC_LOAD     = $(CC) $(CCFLAGS) 

.c.o:
	$(CC_COMPILE) $*.c

EXE = harm
all: $(EXE) image_interp


SRCS = \
bounds.c coord.c diag.c dump.c fixup.c \
image.c init.c interp.c main.c metric.c lu.c \
phys.c ranc.c restart.c step_ch.c \
utoprim_1dfix1.c utoprim_1dvsq2fix1.c utoprim_2d.c u2p_util.c

OBJS = \
bounds.o coord.o diag.o dump.o fixup.o \
image.o init.o interp.o main.o metric.o lu.o \
phys.o ranc.o restart.o step_ch.o \
utoprim_1dfix1.o utoprim_1dvsq2fix1.o utoprim_2d.o u2p_util.o

INCS = decs.h  defs.h  u2p_defs.h  u2p_util.h

$(OBJS) : $(INCS) makefile

$(EXE): $(OBJS) $(INCS) makefile
	$(CC_LOAD) $(OBJS) $(EXTRALIBS) -o $(EXE)


image_interp: image_interp.c
	$(CC_LOAD) $(EXTRALIBS) image_interp.c -o image_interp

clean:
	/bin/rm -f *.o *.il
	/bin/rm -f $(EXE) image_interp


newrun:
	/bin/rm -rf dumps images ener.out
