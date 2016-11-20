project(groff)

cmake_minimum_required(VERSION 2.4.0)

include(darling_exe)

include_directories(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}/src/src/include)
include_directories(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}/gen/include)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/include/FreeBSD)

add_definitions(-DHAVE_CONFIG_H -D__GETOPT_PREFIX=groff_ -D_LIBC)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc -fwrapv -fPIC -ggdb -Wno-implicit-function-declaration -Wno-int-conversion")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdinc -nostdinc++ -fPIC -Wno-missing-exception-spec -Wno-unused-value")
set(CMAKE_SHARED_LINKER_FLAGS "-nodefaultlibs -nostdlib -fPIC -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")
set(CMAKE_EXE_LINKER_FLAGS "-nodefaultlibs -nostdlib -fPIC -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")

SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/darling")
SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

set(libgroff_sources
	src/src/libs/libgroff/assert.cpp
	src/src/libs/libgroff/change_lf.cpp
	src/src/libs/libgroff/cmap.cpp
	src/src/libs/libgroff/color.cpp
	src/src/libs/libgroff/cset.cpp
	src/src/libs/libgroff/device.cpp
	src/src/libs/libgroff/errarg.cpp
	src/src/libs/libgroff/error.cpp
	src/src/libs/libgroff/fatal.cpp
	src/src/libs/libgroff/filename.cpp
	src/src/libs/libgroff/font.cpp
	src/src/libs/libgroff/fontfile.cpp
	src/src/libs/libgroff/geometry.cpp
	src/src/libs/libgroff/getopt.c
	src/src/libs/libgroff/getopt1.c
	src/src/libs/libgroff/glyphuni.cpp
	src/src/libs/libgroff/htmlhint.cpp
	src/src/libs/libgroff/hypot.cpp
	src/src/libs/libgroff/iftoa.c
	src/src/libs/libgroff/invalid.cpp
	src/src/libs/libgroff/lf.cpp
	src/src/libs/libgroff/lineno.cpp
	src/src/libs/libgroff/macropath.cpp
	src/src/libs/libgroff/matherr.c
	src/src/libs/libgroff/maxfilename.cpp
	src/src/libs/libgroff/maxpathname.cpp
	src/src/libs/libgroff/mksdir.cpp
	src/src/libs/libgroff/nametoindex.cpp
	src/src/libs/libgroff/new.cpp
	src/src/libs/libgroff/paper.cpp
	src/src/libs/libgroff/prime.cpp
	src/src/libs/libgroff/progname.c
	src/src/libs/libgroff/ptable.cpp
	src/src/libs/libgroff/quotearg.c
	src/src/libs/libgroff/relocate.cpp
	src/src/libs/libgroff/searchpath.cpp
	src/src/libs/libgroff/spawnvp.c
	src/src/libs/libgroff/string.cpp
	src/src/libs/libgroff/strsave.cpp
	src/src/libs/libgroff/symbol.cpp
	src/src/libs/libgroff/tmpfile.cpp
	src/src/libs/libgroff/tmpname.cpp
	src/src/libs/libgroff/unicode.cpp
	src/src/libs/libgroff/uniglyph.cpp
	src/src/libs/libgroff/uniuni.cpp
	gen/version-libgroff.cpp
)

add_library(groff STATIC ${libgroff_sources})

#add_darling_executable(man ${man_sources})
#target_link_libraries(man system)

#install(TARGETS man DESTINATION libexec/darling/usr/bin)

# Static content
install(DIRECTORY gen/usr DESTINATION libexec/darling)