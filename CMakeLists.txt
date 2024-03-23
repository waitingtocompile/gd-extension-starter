
cmake_minimum_required(VERSION 3.22)

if(APPLE)
    set(CMAKE_OSX_ARCHITECTURES "x86_64;arm64" CACHE STRING "")
endif()

set(PROJECT_VERSION 0.1)

project(
    YOUR_PROJECT_NAME_HERE
    VERSION ${PROJECT_VERSION}
    DESCRIPTION "A c++ godot extension"
    LANGUAGES CXX
)

if(NOT DEFINED CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

#EXTENSION_NAME is the name that should be given to the extension, this will normally be the same as the project name
set(EXTENSION_NAME ${PROJECT_NAME})

#the version of godot we should use the gdextension bindings for (and by extension, the minimum version of godot we support)
set(EXTENSION_COMPATABILITY_MINIMUM 4.2)

#the directory to look in for a godot project (by default the same as the project name)
set(GODOT_PROJECT ${PROJECT_NAME})

#the directory in the godot project to put extension binaries in 
set(GODOT_PROJECT_BIN "bin")

set(GODOT_PROJECT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/${GODOT_PROJECT})

set(OUTPUT_DIR ${GODOT_PROJECT_DIR}/${GODOT_PROJECT_BIN})

option(EXTENSION_HOT_RELOADABLE "Build the gdextension libraries and extension manifest file to enable hot reloading" OFF)

add_subdirectory(dependencies/godot-cpp)

add_subdirectory(extension)

#TODO:copying supporting files (such as icons)
#TODO:packaging into a self-contained blob that can be dropped into other projects or published
#TODO:install target?
