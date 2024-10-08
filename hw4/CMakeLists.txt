cmake_minimum_required(VERSION 2.8)
project(vo_simulate)

add_definitions(-DWORKSPACE_DIR="${CMAKE_SOURCE_DIR}")

set(CMAKE_BUILD_TYPE release)
set(CMAKE_CXX_FLAGS "-std=c++11")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall -O0 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O0 -march=native")

set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g")
MESSAGE("PROJECT_SOURCE_DIR " ${PROJECT_SOURCE_DIR})


find_package(OpenCV 3.1)
if(NOT OpenCV_FOUND)
   find_package(OpenCV 2.4.9)
   if(NOT OpenCV_FOUND)
      message(FATAL_ERROR "OpenCV > 2.4.9 not found.")
   endif()
endif()

find_package(Eigen3  REQUIRED)

include_directories(${PROJECT_SOURCE_DIR} ${PROJECT_SOURCE_DIR}/src)
include_directories(${EIGEN3_INCLUDE_DIR})
include_directories(${OPENCV_INCLUDE_DIR})

add_executable(vo_simulate  demo/main.cpp src/two_view_geometry.cpp src/utils.cpp src/optimizer.cpp)
target_link_libraries(vo_simulate ${OpenCV_LIBS} ${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o.so)