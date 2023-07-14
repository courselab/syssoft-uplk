#  Makefile - Make script.
# 
#   Copyright (c) <YEAR>, <AUTHOR> 
#
#   This piece of software is a derivative work of SYSeg, by Monaco F. J.
#   SYSeg is distributed under the license GNU GPL v3, and is available
#   at the official repository https://www.gitlab.com/monaco/syseg.
#
#   This file is part of <PROJECT>.
#
#   <PROJECT> is free software: you can redistribute it and/or modify
#   it under the terms of the GNU General Public License as published by
#   the Free Software Foundation, either version 3 of the License, or
#   (at your option) any later version.
#   
#   This program is distributed in the hope that it will be useful,
#   but WITHOUT ANY WARRANTY; without even the implied warranty of
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#   
#   You should have received a copy of the GNU General Public License
#   along with this program.  If not, see <http://www.gnu.org/licenses/>.




init: all 


# Update Makefile from Makefile.m4 if needed, and then invoke make again.
# If the source is from a pack-distribution, the lack of Makefile.m4
# inhibits the updating. 

ifndef UPDATED
#$(MAKECMDGOALS) : Makefile #### I removed this May 10, 2023.

Makefile_deps = Makefile.m4 ../../tools/docm4.m4 ../../tools/bintools.m4 ../../tools/Makegyver.mk

Makefile : $(shell if test -f Makefile.m4; then echo $(Makefile_deps); fi);
	@if ! test -f .dist; then\
	  cd .. && make;\
	  make -f Makefile clean;\
	  make -f Makefile UPDATED=1 $(MAKECMDGOAL);\
	fi

endif


##
## Relevant rules
##

all:

.PHONY: clean

clean :

#
# Programming exercise
#


EXPORT_FILES  = check.sh docrypt encrypt libauth.so.md5 test.cry sample.cry
EXPORT_FILES += Makefile README credentials.cry   docrypt.md5   libauth.so   libmylib.so 
EXPORT_FILES += README ../../tools/COPYING 



# Self-contained pack distribution.
#
# make syseg-export     creates a tarball with the essential files, which
#       	        can be distributed independently of the rest of
#			this project.
#
# A pack distribution contain all the items necessary to build and run the
# relevant piece of software. It's useful,a for instance, to bundle
# self-contained subsections of SYSeg meant to be delivered as
# programming exercise assignments or illustrative source code examples.
#		
# In order to select which files should be included in the pack, list them
# in the appropriate variables
# 
# EXPORT_FILES_C    = C files (source, headers, linker scripts)
# EXPORT_FILES_MAKE = Makefiles
# EXPORT_FILES_TEXT = Text files (e.g. README)
# EXPORT_FILES_SH   = Shell scripts (standard /bin/sh)
#
# Except by text files, all other files will have their heading comment
# (the very first comment found in the file) replaced by a corresponding
# standard comments containing boilerplate copyright notice and licensing
# information, with blank fields to be filled in by the pack user.
# Attribution to SYSeg is also included for convenience.

TARNAME=hack01-0.1.0



syseg-export export:
	@if ! test -f .dist; then\
	  make do_export;\
	 else\
	  echo "This is a distribution pack already. Nothing to be done.";\
	fi

do_export:
	rm -rf $(TARNAME)
	mkdir $(TARNAME)
	(cd .. && make clean && make)
	for i in $(EXPORT_FILES); do\
	  ../../tools/syseg-export $$i $(TARNAME);\
	done
	touch $(TARNAME)/.dist
	tar zcvf $(TARNAME).tar.gz $(TARNAME)

clean-export:
	rm -f $(TARNAME).tar.gz
	rm -rf $(TARNAME)

.PHONY: syseg-export export clean-export




