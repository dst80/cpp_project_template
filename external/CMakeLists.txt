#external ist used to avoid multiple duplication of third-party libs on my system. 
#I prefer a enviromental variable for the location of my third-party folder
set(THIRD_PARTY_PATH $ENV{THIRD_PARTY_PATH})
if (WIN32)
    if (${THIRD_PARTY_PATH} STREQUAL "")
        message(FATAL_ERROR "Please add a THIRD_PARTY_PATH environment variable ")
    endif ()
else ()
    if ($ENV{THIRD_PARTY_PATH} STREQUAL "")
        set (THIRD_PARTY_PATH "/usr/local") # default path for arch linux 
    endif()
endif()

if (${PACKAGE_TESTS})
    # currently work for GTest 1.8. Remove this if using single header 
    if (WIN32)
        if(CMAKE_SYSTEM_PROCESSOR STREQUAL "AMD64")
            set (GTest_ROOT "${THIRD_PARTY_PATH}googletest/lib/x64")
        else ()
            set (GTest_ROOT "${THIRD_PARTY_PATH}googletest/lib/x86")
        endif ()
    else ()
        set (GTest_ROOT "${THIRD_PARTY_PATH}")
    endif ()

    find_package (GTest REQUIRED)
    if (NOT ${GTEST_FOUND})
        message (FATAL_ERROR "GoogleTest not found")
    endif ()

    set (GTEST_INCLUDE_DIRS ${GTEST_INCLUDE_DIR} PARENT_SCOPE)      # Use PARENT_SCOPE to use it in the test folder
    set (GTEST_BOTH_LIBRARIES ${GTEST_BOTH_LIBRARIES} PARENT_SCOPE) # Use PARENT_SCOPE to use it in the test folder
endif ()