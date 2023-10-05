cmake_minimum_required(VERSION 3.5)
project(zynmixer)

include(CheckIncludeFiles)
include(CheckLibraryExists)
find_package(PkgConfig REQUIRED)

pkg_check_modules(JACK REQUIRED IMPORTED_TARGET jack)

add_library(zynmixer SHARED mixer.h mixer.c tinyosc.h tinyosc.c)
target_link_libraries(zynmixer PkgConfig::JACK)

install(TARGETS zynmixer LIBRARY DESTINATION lib)
