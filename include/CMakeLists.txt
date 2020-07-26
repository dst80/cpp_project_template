#add here additional subdirectories 

#add here the files in the current directory
set(${PROJECT_NAME}_INCLUDE_FILES
   )


#merge all include files for the current child subdirectories
set(${PROJECT_NAME}_ALL_INCLUDE_FILES
    ${${PROJECT_NAME}_INCLUDE_FILES}
    PARENT_SCOPE)
