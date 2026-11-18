cmake_minimum_required(VERSION 3.21)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_VISIBILITY_PRESET hidden)

project(PassLOCK VERSION 1.0.0)

# Find all C++ source files inside src/
file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS src/*.cpp)

# Create the mod
add_library(${PROJECT_NAME} SHARED ${SOURCES})

# Find the Geode SDK
if (NOT DEFINED ENV{GEODE_SDK})
    message(FATAL_ERROR "Unable to find Geode SDK! Please define GEODE_SDK.")
else()
    message(STATUS "Found Geode SDK: $ENV{GEODE_SDK}")
endif()

# Include Geode
add_subdirectory($ENV{GEODE_SDK} ${CMAKE_CURRENT_BINARY_DIR}/geode)

# Set up the mod
setup_geode_mod(${PROJECT_NAME})
