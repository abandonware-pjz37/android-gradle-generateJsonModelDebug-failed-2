cmake_minimum_required(VERSION 3.9.2)

set(HUNTER_ROOT "${CMAKE_CURRENT_LIST_DIR}/__HUNTER" CACHE PATH "...")
option(HUNTER_STATUS_DEBUG "..." ON)

set(
    HUNTER_ROOT
    "${CMAKE_CURRENT_LIST_DIR}/__HUNTER"
    CACHE
    PATH
    "Hunter root"
)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/forexample/android-gradle-generateJsonModelDebug-failed-2/releases/download/v0.0/hunter-wo.web.zip"
    SHA1 "87420ebc202964a64e4e2ad5025697f0803949b0"
)

set(gen_toolchain "${CMAKE_CURRENT_BINARY_DIR}/generated/toolchain.cmake")
file(TO_CMAKE_PATH "${CMAKE_TOOLCHAIN_FILE}" CMAKE_TOOLCHAIN_FILE_CMAKE_PATH)
configure_file(
  "${CMAKE_CURRENT_LIST_DIR}/toolchain.cmake.in"
  "${gen_toolchain}"
  @ONLY
  )
set(CMAKE_TOOLCHAIN_FILE "${gen_toolchain}" CACHE PATH "" FORCE)

project(foo)
hunter_add_package(OpenCV)
