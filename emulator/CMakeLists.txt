project(gbc-emu C)

cmake_minimum_required(VERSION 3.26 FATAL_ERROR)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

set(CMAKE_BUILD_TYPE Debug)

#######################################################

# include CMake macros
include(CheckIncludeFiles)
include(CheckTypeSize)

#######################################################

# Define macro to check for headers
# check if a ';' separated list of header files may
# may be included together in a source file and store
# the result in the second variable. If true add the
# passed in header file to the ${INCLUDES} variable
set(INCLUDES "")
macro(ck_check_include_file header var)
    check_include_files("${INCLUDES};${header}" ${var})
    if(${var})
        set(INCLUDES ${INCLUDES} ${header})
    endif(${var})
endmacro(ck_check_include_file)

ck_check_include_file("stdlib.h" HAVE_STDLIB_H)

#######################################################

# The Check unit test library requires a few integer types
# in order to work properly. CheckTypeSize checks if the
# type exists, determines it's size and stores it in the
# second parameter passed
check_type_size(intmax_t INTMAX_T)
check_type_size(uintmax_t UINTMAX_T)
# according to the GNU library the pid_t data type is the
# same as an int
check_type_size(pid_t PID_T)
if(NOT HAVE_PID_T)
    if(WIN32)
        set(pid_t "int")
    else(WIN32)
        MESSAGE(FATAL_ERROR "pid_t doesn't exist on this platform")
    endif(WIN32)
endif(NOT HAVE_PID_T)

#######################################################

# Search the CMake Module Path for the 'FindSDL2.cmake' and
# 'FindSDL2_ttf.cmake files 
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/sdl2)
find_package(SDL2 REQUIRED)
find_package(SDL2_ttf REQUIRED)

#######################################################

# Generate config file here...

#######################################################

# Subdirectories
add_subdirectory(lib)
add_subdirectory(gbc-emulator)
add_subdirectory(tests)

#######################################################

# Unit tests
enable_testing()
add_test(NAME check_gbc_emu COMMAND check_gcb_emu)