cmake_minimum_required(VERSION 2.8.11 FATAL_ERROR)

set(gmodule_SOURCES
    src/packet.c
)

set(gmodule_INCLUDES
    include
)

# Iterate each include file and add it to packet_INCLUDE_FILES
foreach(INCLUDE_PATH ${gmodule_INCLUDES})
    file(GLOB_RECURSE INCLUDE_FILES ${INCLUDE_PATH}/*)

    list(APPEND gmod_INCLUDE_FILES ${INCLUDE_FILES})
endforeach(INCLUDE_PATH)

# Add source to library
add_library(gmodule INTERFACE)

# Add include directories to library
target_include_directories(gmodule INTERFACE ${gmodule_INCLUDES})
