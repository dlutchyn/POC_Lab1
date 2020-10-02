cmake_minimum_required(VERSION 3.16)
project(cmake_library C)

set(CMAKE_C_STANDARD 99)
set(LIB zlib)
# встановлення шляху до директорії інсталяції
SET(CMAKE_INSTALL_PREFIX ../installed_lib)

SET(LIBRARY_SOURCES adler32.c compress.c crc32.c deflate.c gzclose.c gzlib.c gzread.c gzwrite.c infback.c inffast.c inflate.c inftrees.c trees.c uncompr.c zutil.c)
SET(LIBRARY_HEADERS crc32.h deflate.h gzguts.h inffast.h inffixed.h inflate.h inftrees.h trees.h zconf.h zlib.h zutil.h)

if(MSVC)
		set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
endif()

add_library(${LIB} STATIC ${LIBRARY_SOURCES} ${LIBRARY_HEADERS})
add_library(dynamic_${LIB} SHARED ${LIBRARY_SOURCES} ${LIBRARY_HEADERS})
set_target_properties(dynamic_${LIB} PROPERTIES OUTPUT_NAME ${LIB})

set(${LIB}_INCLUDE_PATH "include")
target_include_directories(${LIB} PUBLIC
	"$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
	"$<INSTALL_INTERFACE:$<INSTALL_PREFIX>/${functions_INCLUDE_PATH}>")

install(TARGETS ${LIB} DESTINATION lib EXPORT ${LIB})
install(TARGETS dynamic_${LIB} DESTINATION lib EXPORT ${LIB})
install(EXPORT ${LIB} DESTINATION lib/${LIB})
install(FILES ${LIBRARY_HEADERS} DESTINATION ${zlib_INCLUDE_PATH})
