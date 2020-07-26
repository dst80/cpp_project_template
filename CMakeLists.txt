cmake_minimum_required (VERSION 3.14)

project (template_project)  # rename the project here

option (PACKAGE_TESTS "build with tests" ON)
option (BUILD_MT "build with static linking on msvc" ON)

set (CMAKE_CXX_STANDARD 14)
set (CMAKE_CXX_STANDARD_REQUIRED ON)
set (CMAKE_CXX_EXTENSIONS OFF)

#define max warning level to build clean code
if(MSVC)
  add_compile_options(/W4 /WX)
else()
  add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()

#setting required for clang-tidy and clang-format
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

#replace default build flag when building statically
#When using CMake 3.15 use MSVC_RUNTIME_LIBRARY functionality of CMake instead
if(MSVC)
  if (BUILD_MT)
    set(CompilerFlags
            CMAKE_CXX_FLAGS
            CMAKE_CXX_FLAGS_DEBUG
            CMAKE_CXX_FLAGS_RELEASE
            CMAKE_CXX_FLAGS_MINSIZEREL
            CMAKE_CXX_FLAGS_RELWITHDEBINFO
            CMAKE_C_FLAGS
            CMAKE_C_FLAGS_DEBUG
            CMAKE_C_FLAGS_RELEASE
            CMAKE_C_FLAGS_MINSIZEREL
            CMAKE_C_FLAGS_RELWITHDEBINFO
        )
    # Force to use MT
    foreach(CompilerFlag ${CompilerFlags})
        string(REPLACE "/MD" "/MT" ${CompilerFlag} "${${CompilerFlag}}")
        set(${CompilerFlag} "${${CompilerFlag}}" CACHE STRING "msvc compiler flags" FORCE)
        message("MSVC flags: ${CompilerFlag}:${${CompilerFlag}}")
    endforeach()
  endif()
endif()

#required order of including the subdirectories
add_subdirectory("external")
add_subdirectory("include")
add_subdirectory ("source")


if (${PACKAGE_TESTS})
    enable_testing ()
    add_subdirectory (tests)
endif()


