# Makefile for program dr3m
#
# History:  95/12/08 kmflynn

# pathname
WrdA = /usr/opt/wrdapp

# Compiler flags (Fortran - Green Hills):
#    C - check subranges and array bounds
#    u - default data type for undeclareds is undefined
#    g - generate source level symbolic debug information
#   OM - optimization
# (NOTE: set OptDbg to: OptM to generate optimized code
#                       DbgF to generate debug code)
DbgF   = -g
OptM   = -OM
OptDbg =
FFLAGS = -C -u $(OptDbg)

# Compiler name
F77 = f77

# this description file uses the Bourne shell
SHELL = /bin/sh

#*******************************************************************
#***** You should not need to modify anything below this line. *****
#*******************************************************************

# library directory
library = $(WrdA)/lib3.0
LibDir  = $(WrdA)/lib3.0/lib

program = dr3m

Objects = drmain.o  drfile.o drinput.o \
          drsimul.o drdfwv.o drflow.o  droptmz.o droutpt.o
Libs    = $(LibDir)/wdmlib.a $(LibDir)/adwdmlib.a $(LibDir)/utillib.a

BINDIR  = ../bin
binary  = ../bin
binMake = $(binary)/$(program)
binInst = $(BINDIR)/$(program)

# Rules
all:  first $(binMake) install
	@echo "\n"Done making all, files are now up to date."\n"

# program dependencies
$(binMake):  $(Objects) $(Libs)
	$(F77) $(Objects) $(Libs) -o $@

first:
	@if [ ! -d $(binary) ]   ; then        \
	   mkdir $(binary)  ;                  \
	   echo Created directory $(binary) ;  \
	fi
install:
# Create directory for binary file, if necessary
	@if [ ! -d $(BINDIR) ]   ; then        \
	   mkdir $(BINDIR) ;                   \
	   echo  Created directory $(BINDIR) ; \
	fi
# Link executable to BINDIR if installing elsewhere
	@if [ ! -s $(binMake) ] ; then                              \
	   echo program $(binMake) does not exist, ;                \
	   echo use one of the following commands to generate it:;  \
	   echo "     make" ;  echo "     make all" ;               \
	else                                                        \
	   if [ $(BINDIR) != $(binary) ] ; then                \
	      rm -f $(binInst) ;                               \
	      cd .. ; ln -s `pwd`/bin/$(program) $(binInst);   \
	      chmod 644 $(binInst) ;                           \
	      echo "\n"Program $(binInst) has been updated.;   \
	   fi ; \
	fi
clean:
	@if [ $(BINDIR) != $(binary) ] ; then rm -f $(binInst) ; fi
	rm -f *.o $(binMake)
	@echo Removed files generated by make."\n"

# Define object file dependencies:
drdfwv.o:  pinout.inc
drfile.o:  cf1a3.inc  fmessg.inc pinout.inc plimt.inc  xrecl.inc
drflow.o:  cc3t4.inc  cc7t8.inc  ce1.inc    ce2t3.inc  cf1a3.inc  cinit.inc  \
           cpuls.inc  csgs2.inc  csgs3.inc  csgsc.inc  cstrm.inc  cunit.inc  \
           cuprc.inc  cz1t4.inc  pinout.inc plimt.inc
drinput.o: cc2.inc    cc3t4.inc  cc7t8.inc  cd1.inc    cdeud.inc  ce2t3.inc  \
           cf1a3.inc  chead.inc  cinit.inc  cpuls.inc  csgs1.inc  csgs2.inc  \
           csgs3.inc  csgsc.inc  cstrm.inc  cuprc.inc  cz1t4.inc  pinout.inc \
           plimt.inc
drmain.o:  cc7t8.inc  cd1.inc    cf1a3.inc  chead.inc  csgs1.inc  csgs3.inc  \
           csgsc.inc  cstrm.inc  cunit.inc  cz1t4.inc  dinout.inc pinout.inc \
           plimt.inc  versn.inc
droptmz.o: cz1t4.inc  pinout.inc
droutpt.o: cc7t8.inc  cf1a3.inc  chead.inc  csgs1.inc  csgs2.inc  csgs3.inc  \
           csgsc.inc  cstrm.inc  cunit.inc  cz1t4.inc  pinout.inc plimt.inc
drsimul.o: cc2.inc    cc3t4.inc  cc7t8.inc  cd1.inc    cdeud.inc  ce1.inc    \
           ce2t3.inc  cf1a3.inc  chead.inc  csgs1.inc  csgs2.inc  csgs3.inc  \
           csgsc.inc  cstrm.inc  cunit.inc  cuprc.inc  cz1t4.inc  dstrm.inc  \
           pinout.inc plimt.inc
wdmbat.o:  cdrloc.inc cfbuff.inc cwtsds.inc ctsbuf.inc cwdmid.inc

# end of make
