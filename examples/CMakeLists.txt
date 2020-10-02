cmake_minimum_required(VERSION 3.17)
project(examples C)

set(CMAKE_C_STANDARD 99)
set(LIB zlib)

if(MSVC)
		set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
endif()

# не розпізнає ${LIB}_PREFIX, не знайшов як це 
# пофіксити, тому викристав поточний шлях
# message("path = ${LIB}_PREFIX") вивід: path =
include(${CMAKE_CURRENT_SOURCE_DIR}/../library/installed_lib/lib/${LIB}/${LIB}.cmake)

add_executable(example example.c)
target_include_directories(example PUBLIC ${${LIB}_INCLUDE_DIRS})
target_link_libraries(example ${LIB})

add_executable(minigzip minigzip.c)
target_include_directories(minigzip PUBLIC ${${LIB}_INCLUDE_DIRS})
target_link_libraries(minigzip ${LIB})
