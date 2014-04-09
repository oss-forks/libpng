# CMakeLists.txt

# Copyright (C) 2007-2013 Glenn Randers-Pehrson

# This code is released under the libpng license.
# For conditions of distribution and use, see the disclaimer
# and license in png.h

CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(libpng C)

FIND_PACKAGE(ZLIB REQUIRED)
INCLUDE_DIRECTORIES(${ZLIB_INCLUDE_DIRS})
INCLUDE("${ZLIB_INCLUDE_DIRS}/zlib.cmake" OPTIONAL)

IF(WIN32)
	SET(M_LIBRARY "")
ELSE()
	FIND_LIBRARY(M_LIBRARY NAMES m PATHS /usr/lib /usr/local/lib)
ENDIF()

IF(MSVC)
	ADD_DEFINITIONS(-D_CRT_SECURE_NO_DEPRECATE)
ENDIF()

ADD_LIBRARY(libpng STATIC
	scripts/pnglibconf.h.prebuilt
	png.h
	pngconf.h
	pngdebug.h
	pnginfo.h
	pnglibconf.h
	pngpriv.h
	pngstruct.h
	png.c
	pngerror.c
	pngget.c
	pngmem.c
	pngpread.c
	pngread.c
	pngrio.c
	pngrtran.c
	pngrutil.c
	pngset.c
	pngtrans.c
	pngwio.c
	pngwrite.c
	pngwtran.c
	pngwutil.c
)

SET_TARGET_PROPERTIES(libpng PROPERTIES PREFIX "")
TARGET_LINK_LIBRARIES(libpng ${ZLIB_LIBRARIES} ${M_LIBRARY})
