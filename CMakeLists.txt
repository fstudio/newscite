# top cmake
cmake_minimum_required(VERSION 3.13)

project(NewScite CXX)

if( CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR AND NOT MSVC_IDE )
  message(FATAL_ERROR "In-source builds are not allowed.
CMake would overwrite the makefiles distributed with Privexec.
Please create a directory and run cmake from there, passing the path
to this source directory as the last argument.
This process created the file `CMakeCache.txt' and the directory `CMakeFiles'.
Please delete them.")
endif()


# include(CheckIPOSupported)
# check_ipo_supported(RESULT lto_supported OUTPUT error)
# if(lto_supported)
#   message(STATUS "IPO/LTO enabled")
# else()
#   message(STATUS "IPO/LTO not supported: <${error}>")
# endif()

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17) 
set(CMAKE_CXX_STANDARD_REQUIRED YES)

if(MSVC)
  add_compile_options("-utf-8")
  add_compile_options("-permissive-")
  add_compile_options("-Zc:__cplusplus")
  add_compile_options("-DUNICODE=1")
  add_compile_options("-D_UNICODE=1")
  add_compile_options("-D_CRT_SECURE_CPP_OVERLOAD_STANDARD_NAMES=1")
  add_compile_options("-D_CRT_SECURE_NO_DEPRECATE=1")
  add_compile_options("-D_SCL_SECURE_NO_WARNINGS=1")
  add_compile_options("-DNO_LUA=1")
  add_compile_options("-DSTATIC_BUILD=1")
  set(WIN_COMPILER_FLAGS
    CMAKE_CXX_FLAGS
    CMAKE_CXX_FLAGS_DEBUG
    CMAKE_CXX_FLAGS_RELEASE
    CMAKE_C_FLAGS
    CMAKE_C_FLAGS_DEBUG
    CMAKE_C_FLAGS_RELEASE
  )
  foreach(WIN_COMPILER_FLAG ${WIN_COMPILER_FLAGS})
    string(REPLACE "/MD" "/MT" ${WIN_COMPILER_FLAG} "${${WIN_COMPILER_FLAG}}")
  endforeach()
  #add_compile_definitions()
endif(MSVC)

set(EXECUTABLE_OUTPUT_PATH "${PROJECT_BINARY_DIR}/bin")
set(LIBRARY_OUTPUT_PATH "${PROJECT_BINARY_DIR}/lib")

include_directories(
    scintilla/include
    scintilla/src
    scintilla/lexlib
)

add_subdirectory(scintilla)
add_subdirectory(scite)