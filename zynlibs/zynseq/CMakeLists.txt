cmake_minimum_required(VERSION 3.5)
project(zynseq)

include(CheckIncludeFiles)
include(CheckLibraryExists)
find_package(PkgConfig REQUIRED)

pkg_check_modules(JACK REQUIRED IMPORTED_TARGET jack)

add_library(zynseq SHARED zynseq.h zynseq.cpp sequencemanager.cpp pattern.cpp sequence.cpp timebase.cpp track.cpp)
target_link_libraries(zynseq PkgConfig::JACK)

install(TARGETS zynseq LIBRARY DESTINATION lib)
