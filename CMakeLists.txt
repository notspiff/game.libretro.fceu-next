project(gameclient.fceu-next)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(xbmc REQUIRED)

include(ExternalProject)

externalproject_add(fceu-next
                    GIT_REPOSITORY https://github.com/libretro/fceu-next
                    GIT_TAG 66eb5fb
                    PREFIX fceu-next
                    PATCH_COMMAND patch -p1 < ${PROJECT_SOURCE_DIR}/00_rename_file.patch
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make -f Makefile.libretro-fceux
                    BUILD_IN_SOURCE 1)

set(FCEU-NEXT_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/fceu-next/src/fceu-next/libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                            fceumm_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} fceu-next)

build_addon(gameclient.fceu-next FCEU-NEXT DEPLIBS)
add_dependencies(gameclient.fceu-next fceu-next)
