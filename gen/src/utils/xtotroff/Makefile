# Copyright (C) 2004
#   Free Software Foundation, Inc.
#      Written by James Clark (jjc@jclark.com)
#
# This file is part of groff.
#
# groff is free software; you can redistribute it and/or modify it under
# the terms of the GNU General Public License as published by the Free
# Software Foundation; either version 2, or (at your option) any later
# version.
#
# groff is distributed in the hope that it will be useful, but WITHOUT ANY
# WARRANTY; without even the implied warranty of MERCHANTABILITY or
# FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
# for more details.
#
# You should have received a copy of the GNU General Public License along
# with groff; see the file COPYING.  If not, write to the Free Software
# Foundation, 51 Franklin St - Fifth Floor, Boston, MA 02110-1301, USA.

builddir=/Users/ariel/git/darling/src/external/groff/gen/src/utils/xtotroff
top_srcdir=/Users/ariel/git/darling/src/external/groff/gen/src/utils/xtotroff/../../../../groff
top_builddir=/Users/ariel/git/darling/src/external/groff/gen/src/utils/xtotroff/../../../.
SHELL=/bin/sh

devdir=$(top_builddir)/font
driverdir=$(top_srcdir)/src/devices/xditview
mkinstalldirs=$(SHELL) $(top_srcdir)/mkinstalldirs

xtotroff=$(builddir)/xtotroff
DPIS=75 100

all:
	@echo "Say \`make fonts' to generate fonts for gxditview."

fonts: $(xtotroff) $(driverdir)/DESC.in $(driverdir)/FontMap
	fonts=`sed -e 's/[	 ].*//' $(driverdir)/FontMap`; \
	for dpi in $(DPIS); do \
	  echo Making devX$$dpi; \
	  test -d $(devdir)/devX$$dpi || \
	    $(mkinstalldirs) $(devdir)/devX$$dpi; \
	  rm -f $(devdir)/devX$$dpi/DESC; \
	  sed -e "s/res 75/res $$dpi/" $(driverdir)/DESC.in \
	    >$(devdir)/devX$$dpi/DESC; \
	  (cd $(devdir)/devX$$dpi; \
	   rm -f Makefile.sub; \
	   echo DEV=X$$dpi >Makefile.sub; \
	   echo DEVFILES=DESC $$fonts >>Makefile.sub; \
	   $(xtotroff) -r $$dpi -s 10 $(driverdir)/FontMap); \
	  echo Making devX$$dpi-12; \
	  test -d $(devdir)/devX$$dpi-12 || \
	    $(mkinstalldirs) $(devdir)/devX$$dpi-12; \
	  rm -f $(devdir)/devX$$dpi-12/DESC; \
	  sed -e "s/res 75/res $$dpi/" \
	      -e 's/unitwidth 10/unitwidth 12/' $(driverdir)/DESC.in \
	    >$(devdir)/devX$$dpi-12/DESC; \
	  (cd $(devdir)/devX$$dpi-12; \
	   rm -f Makefile.sub; \
	   echo DEV=X$$dpi-12 >Makefile.sub; \
	   echo DEVFILES=DESC $$fonts >>Makefile.sub; \
	   $(xtotroff) -r $$dpi -s 12 $(driverdir)/FontMap); \
	done
