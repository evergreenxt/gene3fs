#
#
# Makefile.am:
#
#
# $Id:$
#
# $Log:$
#
#
#

#
# Copyright (c) 2012 Citrix Systems, Inc.
# 
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2.1 of the License, or (at your option) any later version.
# 
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
# 
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
#


SRCS= libbudgetvhd.c version.c swab.c

BUDGETVHDSRCS=${SRCS}

noinst_HEADERS= internal.h 

libbudgetvhd_la_SOURCES = ${BUDGETVHDSRCS}

BUILT_SOURCES = version.h budgetvhd.h

lib_LTLIBRARIES=libbudgetvhd.la

include_HEADERS=budgetvhd.h

AM_CFLAGS=-g -Wall -fvisibility=hidden 

libbudgetvhd_la_LDFLAGS = \
        -version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE) \
        -release $(LT_RELEASE) \
        -export-dynamic 

VFD=${srcdir}/..
VF=${shell cat ${VFD}/version-files}
VFS=${VF:%=${VFD}/%}
VCHK=${shell cat ${VFS} | @MD5SUM@ | @AWK@ '{print $$1 }' }
VNUM=${shell @GREP@ ${VCHK} ${VFD}/version-md5sums | @AWK@ '{ print $$2 }'  }
VDEF=${shell echo `cat ${VFD}/version-major`.`cat ${VFD}/version-minor`.`cat ${VFD}/version-micro` }


version.h: $(VFD)/version-files $(VFD)/version-major \
	$(VFD)/version-minor $(VFD)/version-micro \
	$(VFD)/version-md5sums ${VFS} Makefile
	if [ .${VNUM} = . ]; then \
		echo "#define FULL_VERSION \"libbudgetvhd Version ${VDEF} + Edits\"" > version.h; \
		echo ${VDEF}-E > version-num; \
	else \
		echo "#define FULL_VERSION \"libbudgetvhd Version ${VNUM}\"" > version.h; \
		echo ${VNUM} > version-num; \
	fi

