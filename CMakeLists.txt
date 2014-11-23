cmake_minimum_required(VERSION 2.8.9)

project(zlib C)


include_directories(${CMAKE_CURRENT_BINARY_DIR})


#============================================================================
# zlib
#============================================================================

set(ZLIB_PUBLIC_HDRS
    zconf.h
    zlib.h
)
set(ZLIB_PRIVATE_HDRS
    contrib/minizip/unzip.h
    contrib/minizip/zip.h
    crc32.h
    deflate.h
    inffast.h
    inffixed.h
    inflate.h
    inftrees.h
    mozzconf.h
    trees.h
    zutil.h
)
set(ZLIB_SRCS
    contrib/minizip/unzip.c
    contrib/minizip/zip.c
    adler32.c
    compress.c
    crc32.c
    deflate.c
    gzio.c
    infback.c
    inffast.c
    inflate.c
    inftrees.c
    trees.c
    uncompr.c
    zutil.c
)

if(WIN32)
    set(ZLIB_PRIVATE_HDRS ${ZLIB_PRIVATE_HDRS} contrib/minizip/iowin32.h)
    set(ZLIB_SRCS ${ZLIB_SRCS} contrib/minizip/iowin32.c)
else()
    set(ZLIB_PRIVATE_HDRS ${ZLIB_PRIVATE_HDRS} contrib/minizip/ioapi.h)
    set(ZLIB_SRCS ${ZLIB_SRCS} contrib/minizip/ioapi.c)
endif()

add_library(zlib ${ZLIB_SRCS} ${ZLIB_PUBLIC_HDRS} ${ZLIB_PRIVATE_HDRS})
set_target_properties(zlib PROPERTIES OUTPUT_NAME z)

