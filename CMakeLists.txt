project(game.libretro.fceu-next)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make -f Makefile.libretro-fceux platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make -f Makefile.libretro-fceux ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make -f Makefile.libretro-fceux platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

include(ExternalProject)
externalproject_add(fceu-next
                    GIT_REPOSITORY https://github.com/libretro/fceu-next
                    GIT_TAG 66eb5fb
                    PREFIX fceu-next
                    PATCH_COMMAND patch -p1 < ${PROJECT_SOURCE_DIR}/00_rename_file.patch
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(FCEU-NEXT_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/fceu-next/src/fceu-next/libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                            game.libretro.fceu-next${CMAKE_SHARED_LIBRARY_SUFFIX} fceu-next)

build_addon(game.libretro.fceu-next FCEU-NEXT DEPLIBS)
add_dependencies(game.libretro.fceu-next fceu-next)

include(CPack)
