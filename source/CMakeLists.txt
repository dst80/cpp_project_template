# add here subdirectory


#current path source directory
include_directories("${PROJECT_SOURCE_DIR}/include/")

#current path source directory
set(${PROJECT_NAME}_SOURCE_FILES
    )

#add source file here
set(${PROJECT_NAME}_ALL_SOURCE_FILES
    )

#build testable lib
add_library(${PROJECT_NAME}_lib STATIC "${${PROJECT_NAME}_ALL_SOURCE_FILES}" "${${PROJECT_NAME}_ALL_INCLUDE_FILES}")

#build executable if required
#add_executable(${PROJECT_NAME} STATIC "main.cpp" "${${PROJECT_NAME}_lib})