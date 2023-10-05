cmake_minimum_required(VERSION 3.5)
# set(CMAKE_VERBOSE_MAKEFILE ON)

project(zynaudioplayer)

option(ENABLE_OSC "Enable OSC support" TRUE)

include(CheckIncludeFiles)
include(CheckLibraryExists)
find_package(PkgConfig REQUIRED)


pkg_check_modules(Libs REQUIRED IMPORTED_TARGET jack sndfile samplerate rubberband)

if(ENABLE_OSC)
	message("OSC enabled")
	add_definitions(-DENABLE_OSC)
	add_library(zynaudioplayer SHARED player.cpp tinyosc.c)
		target_link_libraries(zynaudioplayer pthread)
		target_link_libraries(zynaudioplayer PkgConfig::Libs)
else()
	message("OSC disabled")
	add_library(zynaudioplayer SHARED player.cpp)
		target_link_libraries(zynaudioplayer pthread)
		target_link_libraries(zynaudioplayer PkgConfig::Libs)
endif()

install(TARGETS zynaudioplayer LIBRARY DESTINATION lib)
