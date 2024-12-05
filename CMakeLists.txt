cmake_minimum_required(VERSION 3.19)
 
#[===[ Basic Project Configuration ]===]
 
project("AdventOfCode"
    LANGUAGES CXX
)
 
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
 
add_compile_definitions(LIBCXX_ENABLE_INCOMPLETE_FEATURES=ON)
 
set(CMAKE_CXX_STANDARD 20)
 
include("CTest")
 
#[===[ Policies ]===]
 
if(POLICY CMP0135)
  cmake_policy(SET CMP0135 NEW)
endif()
 
if(POLICY CMP0167)
  cmake_policy(SET CMP0167 NEW)
endif()
 
#[===[ Third-party dependencies ]===]
 
add_subdirectory("lib")
 
Include(FetchContent)
 
FetchContent_Declare(
  "Catch2"
  URL "https://github.com/catchorg/Catch2/archive/refs/tags/v3.7.0.zip"
  URL_HASH "SHA256=75b04c94471a70680f10f5d0d985bd1a96b8941d040d6a7bfd43f6c6b1de9daf"
  EXCLUDE_FROM_ALL
  FIND_PACKAGE_ARGS
)
 
FetchContent_Declare(
  "boost"
  URL "https://github.com/boostorg/boost/releases/download/boost-1.86.0/boost-1.86.0-cmake.zip"
  URL_HASH "SHA256=a66084ec52c9dfa838b3b225a29f29869b2d11e201b3f9e4b989431d95b671c2"
  EXCLUDE_FROM_ALL
  FIND_PACKAGE_ARGS
)
 
FetchContent_MakeAvailable(
  "Boost"
  "Catch2"
)
 
find_package("Boost" REQUIRED "1.86")
find_package("Catch2" REQUIRED "3.7.0" )
 
include("Catch")
 
#[===[ Per-day Subdirectories ]===]
 
file(GLOB ADVENT_OF_CODE_DAYS
    RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}"
    CONFIGURE_DEPENDS
    "day*/CMakeLists.txt"
)
 
foreach(DAY IN LISTS ADVENT_OF_CODE_DAYS)
    get_filename_component(DAY "${DAY}" DIRECTORY)
    add_subdirectory("${DAY}")
endforeach()