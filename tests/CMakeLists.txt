# add here the unit test subdirectories

#current path source directory
set (${PROJECT_NAME}_UNITTEST_SOURCE_FILES
    )


#add source file here
set (${PROJECT_NAME}_UNITTEST_ALL_SOURCE_FILES
    )

# include files 
include_directories (${GTEST_INCLUDE_DIRS})
include_directories ("${PROJECT_SOURCE_DIR}/include")

#build test executable
enable_testing()

add_executable(${PROJECT_NAME}_unit_test ${${PROJECT_NAME}_UNITTEST_ALL_SOURCE_FILES} )

#set executable for c test. Not required if not using ctest
gtest_add_tests(${PROJECT_NAME}_unit_test "" AUTO)

#link with project library
target_link_libraries(${PROJECT_NAME}_unit_test ${PROJECT_NAME}_lib)

#link with google test library
target_link_libraries(${PROJECT_NAME}_unit_test ${GTEST_BOTH_LIBRARIES})
