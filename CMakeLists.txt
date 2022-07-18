# cmake version
cmake_minimum_required(VERSION 3.4)

# compile options
add_compile_options(-Wall -Wextra)

# project information
project(ex_camera)

# depthai package
find_package(depthai CONFIG REQUIRED)
find_package(OpenCV REQUIRED)

# include
include_directories(include)
include_directories(src)



# static library
add_library(RobotCamera
    src/mytest.cpp
    )
target_link_libraries(RobotCamera
    depthai::opencv
    ${OpenCV_LIBS}
    )

# adding the executable file & linking library
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME}
    PUBLIC
        RobotCamera
    )
