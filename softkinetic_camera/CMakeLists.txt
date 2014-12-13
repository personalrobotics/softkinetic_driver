cmake_minimum_required(VERSION 2.8.3)
project(softkinetic_camera)

# find the DepthSense SDK
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")
find_package(catkin REQUIRED COMPONENTS
roscpp
image_transport
tf)
find_package(DepthSenseSDK)
find_package( PCL REQUIRED )


if(NOT DepthSenseSDK_FOUND)
  message(FATAL_ERROR "+++++++++ Could not locate the DepthSense SDK +++++++++
Please install the SDK before trying to build the 'softkinetic_camera' package, see README.txt.

Cannot continue, aborting.")
  return()
endif()

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

include_directories(
  include
  ${DepthSenseSDK_INCLUDE_DIRS}
  ${PCL_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
)

link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
#include_directories(/usr/include/suitesparse)

add_executable(softkinetic_bringup_node src/softkinetic_start.cpp)
target_link_libraries(softkinetic_bringup_node
 ${catkin_LIBRARIES}
 ${DepthSenseSDK_LIBRARIES}
${PCL_LIBRARIES})

