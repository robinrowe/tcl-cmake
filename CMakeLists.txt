# tcl-cmake/CMakeLists.txt

cmake_minimum_required(VERSION 2.8.2)
set(NAME TCL-TK)
project(${NAME})
message("--- Building Project ${NAME} ---")

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")

set(CMAKE_PREFIX_PATH "${CMAKE_CURRENT_SOURCE_DIR}/lib")
set(CMAKE_INCLUDE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/lib")

add_definitions( -DCMAKE_SOURCE_DIR="${CMAKE_SOURCE_DIR}" )

if(WIN32)
	add_definitions(-DPLATFORM_WINDOWS)
else()
    string(TOUPPER "${CMAKE_BUILD_TYPE}" UPPER_BUILD_TYPE)
    if(UPPER_BUILD_TYPE STREQUAL "RELEASE")
        add_definitions(-DNDEBUG)
    else()
        add_definitions(-D_DEBUG -DDEBUG)
    endif()
endif()

set(HAVE_PARENT_BUILD TRUE)
set(TCLMAN_GENERATED TRUE)

set(SUBDIRS tcl tk)
add_subdirectory(${SUBDIRS})