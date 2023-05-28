cmake_minimum_required (VERSION 3.10)

# Set the project name
project(SanitizePlayground
        VERSION 0.0 DESCRIPTION "Sanitize playground")

set(AUTHOR "Uwe Köhler")
set(VERSION_STRING "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}")
# from CMake 3.12
#add_compile_definitions(VERSION_STRING ${VERSION_STRING} )
# inner "" to get C++ to treat definition as a string, outer "" to handle spaces
add_definitions(-D VERSION_STRING="\\"${VERSION_STRING}\\"" -D PROJECT_BIN_DIR="\\"${PROJECT_BINARY_DIR}\\"")
set(CMAKE_CXX_STANDARD 17)

if(NOT DEFINED ENV{GITHUB_ACTIONS})
    # lets see what is actually happening under the hood this is helpful when
    # running into problems
    set(CMAKE_VERBOSE_MAKEFILE ON)
endif()
# Some init settings
set(CMAKE_COLOR_MAKEFILE ON)
# Set path to additional CMake modules
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake ${CMAKE_MODULE_PATH})

message(STATUS "CMAKE_PREFIX_PATH ${CMAKE_PREFIX_PATH}")

include(Sanitize)

# the RPATH to be used when installing, but only if it's not a system directory
LIST(FIND CMAKE_PLATFORM_IMPLICIT_LINK_DIRECTORIES "${CMAKE_INSTALL_PREFIX}/lib" isSystemDir)
IF("${isSystemDir}" STREQUAL "-1")
   SET(CMAKE_INSTALL_RPATH "$ORIGIN/../lib")
ENDIF("${isSystemDir}" STREQUAL "-1")

set(DEBUG_POSTFIX "_g")
if( CMAKE_BUILD_TYPE MATCHES Debug)
    message(STATUS "Debug mode")
endif()

# add the CMakeFile that defines the application and library
add_subdirectory(src)

