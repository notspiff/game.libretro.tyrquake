project(game.libretro.tyrquake)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

include(ExternalProject)
externalproject_add(tyrquake
                    GIT_REPOSITORY https://github.com/libretro/tyrquake
                    GIT_TAG 66a5d56
                    PREFIX tyrquake
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make -f Makefile.libretro
                    BUILD_IN_SOURCE 1)

set(TYRQUAKE_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/tyrquake/src/tyrquake/tyrquake_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                           game.libretro.tyrquake${CMAKE_SHARED_LIBRARY_SUFFIX} tyrquake)

build_addon(game.libretro.tyrquake TYRQUAKE DEPLIBS)
add_dependencies(game.libretro.tyrquake tyrquake)

include(CPack)
