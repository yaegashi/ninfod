#
# Makefile.am
#
# To generage Makefile.in / config.h.in from Makefile.am, invoke
#	aclocal
#	autoheader
#	automake --foreign --add-missing
# To generate Makefile and configure.in, from Makefile, invoke
#	autoconf
#
sbin_PROGRAMS = ninfod
ninfod_SOURCES = ni_ifaddrs.c ninfod.c ninfod_addrs.c ninfod_core.c ninfod_name.c \
	ninfod.h icmp6_nodeinfo.h ni_ifaddrs.h

GIT=git

DEFS=@DEFS@

LASTTAG=`${GIT} describe HEAD | sed -e 's/-s.*//'`
RELEASE=`cat Release`
DATE=`date +%Y%m%d`
VERSION=$(RELEASE)-dirty
DEBVER=$(RELEASE).dirty

mkpkg:
	@date "+[$(VERSION)]" > ChangeLog.NEW
	@echo >>ChangeLog.NEW
	@${GIT} log $(LASTTAG).. | ${GIT} shortlog >> ChangeLog.NEW
	@echo >> ChangeLog.NEW
	@cat ChangeLog >> ChangeLog.NEW
	@mv ChangeLog.NEW ChangeLog 
	@dch --newversion $(DEBVER) "New upstream release."
	@${GIT} commit -a -m "$(PACKAGE)-$(VERSION)"
	@${GIT} tag -s -m "$(BASENAME)-$(VERSION)" $(VERSION)
	$(MAKE) dist
#	@${GIT} archive --format=tar --prefix=$(BASENAME)-$(TAG)/ $(TAG) | bzip2 -9 > ../$(BASENAME)-$(TAG).tar.bz2

snapshot:
	$(MAKE) mkpkg VERSION=s$(DATE) DEBVER=$(RELEASE).$(DATE)

release:
	$(MAKE) mkpkg VERSION=v$(RELEASE) DEBVER=$(RELEASE)

#ninfod: ninfod_addrs.o ni_ifaddrs.o ninfod_name.o ninfod_core.o ninfod.o
#        $(CC) $(LDFLAGS) $^ $(LIBS) -o $@
.c.o:
	$(CC) $(CFLAGS) -c $(DEFS) -o $@ $^

# Copyright (C)2002 USAGI/WIDE Project.
# Copyright (C)2000-2001 Hideaki YOSHIFUJI and USAGI Project.
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
# 3. Neither the name of the project nor the names of its contributors
#    may be used to endorse or promote products derived from this software
#    without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE PROJECT AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED.  IN NO EVENT SHALL THE PROJECT OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.
############################################################################
