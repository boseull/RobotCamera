cmake_minimum_required(VERSION 3.4)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/depthai-core EXCLUDE_FROM_ALL)
project(camera)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror")
set(CMAKE_POSITION_INDEPENDENT_CODE true)


# Add the headers from the <include> directory
include_directories(include/${PROJECT_NAME})
include_directories(src/${PROJECT_NAME})

# Add the source files from the <src> directory
file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
    )

add_library(${PROJECT_NAME}_src ${SRC_FILES})

target_link_libraries(${PROJECT_NAME}_src depthai::opencv ${OS_LIBS})

# Add the executable files
add_executable(${PROJECT_NAME}_test src/${PROJECT_NAME}/main.cpp)
# Linking for libraries
target_link_libraries(${PROJECT_NAME}_test
        ${PROJECT_NAME}_src
    # PRIVATE
        depthai::opencv
        )
