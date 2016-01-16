cmake_minimum_required(VERSION 2.8.11 FATAL_ERROR)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

project(example)

add_subdirectory(.. ${CMAKE_BINARY_DIR}/deps)

set(example_SOURCES
    src/gm_example.cpp
)

add_definitions(-DGMMODULE)

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(PLATFORM_NAME "macosx")
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    set(PLATFORM_NAME "linux")
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    set(PLATFORM_NAME "windows")
else(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(PLATFORM_NAME "unknown")
endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

add_library(example SHARED ${example_SOURCES})

set_target_properties(example PROPERTIES
    COMPILE_FLAGS "-m32"
    LINK_FLAGS "-m32"
    OUTPUT_NAME "example"
    PREFIX "gmsv_"
    SUFFIX "_${PLATFORM_NAME}.dll"
)

target_link_libraries(example gmodule)
