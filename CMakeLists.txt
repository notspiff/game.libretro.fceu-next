project(game.libretro.fceumm)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)
find_package(libretro-fceumm REQUIRED)

set(DEPLIBS fceumm)
set(FCEUMM_CUSTOM_BINARY ${FCEUMM_LIB}
                         game.libretro.fceumm${CMAKE_SHARED_LIBRARY_SUFFIX} fceumm)

build_addon(game.libretro.fceumm FCEUMM DEPLIBS)
