cmake_minimum_required(VERSION 2.8.12)

project(windows-cmake-dll-version)

set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

# Module
include(GenerateExportHeader)
include(generate_product_version)

# VERSION
generate_product_version(
    VersionFilesOutputVariable
    NAME "My Great Project"
    ICON ${PATH_TO_APPLICATION_ICON}
    VERSION_MAJOR 1
    VERSION_MINOR 3
    VERSION_PATH ${BUILD_COUNTER}
    VERSION_REVISION ${BUILD_REVISION}
)

# INCLUDE
include_directories(${CMAKE_BINARY_DIR})

# LIBRARY
add_library(lib SHARED lib.cpp ${VersionFilesOutputVariable})
generate_export_header(lib)

# EXECUTABLE
add_executable(${PROJECT_NAME} main.cpp)