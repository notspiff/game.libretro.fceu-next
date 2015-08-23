project(game.libretro.fceu-next)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)
find_package(fceu-next REQUIRED)

set(DEPLIBS nestopia)
set(FCEU_NEXT_CUSTOM_BINARY ${FCEU_NEXT_LIB}
                           game.libretro.fceu-next${CMAKE_SHARED_LIBRARY_SUFFIX} fceu-next)

build_addon(game.libretro.fceu-next FCEU_NEXT DEPLIBS)