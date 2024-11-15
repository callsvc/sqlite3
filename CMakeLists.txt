cmake_minimum_required(VERSION 3.29)

add_library(sqlite3 SHARED)

target_compile_definitions(sqlite3 PRIVATE SQLITE_THREADSAFE=0 SQLITE_OMIT_DEPRECATED)

if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILED_ID STREQUAL "Clang")
    target_compile_options(sqlite3 PRIVATE -O2 -Wno-stringop-truncation)
endif()

target_sources(sqlite3 PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/src/sqlite3.c
    ${CMAKE_CURRENT_SOURCE_DIR}/include/sqlite3.h
    ${CMAKE_CURRENT_SOURCE_DIR}/include/sqlite3ext.h
)

target_include_directories(sqlite3 PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:>
)

add_library(sqlite3::sqlite3 ALIAS sqlite3)
