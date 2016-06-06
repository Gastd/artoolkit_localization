cmake_minimum_required(VERSION 2.4.6)
project(artoolkit_localization)
# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
find_package(Eigen3 REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  roscpp
  sensor_msgs
  roslib
  tf
)
set(ROS_BUILD_TYPE RelWithDebInfo)

catkin_package(
 INCLUDE_DIRS include
#  LIBRARIES novatel_gps
 CATKIN_DEPENDS geometry_msgs roscpp sensor_msgs ar_pose tf roslib
#  DEPENDS system_lib
)

include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
)
include_directories(/usr/include/eigen3)

add_executable(artoolkit_localization src/localization_node.cpp src/ar_map.cpp src/ukf.cpp)
target_link_libraries(artoolkit_localization ${catkin_LIBRARIES})
