cmake_minimum_required(VERSION 2.8.3)
project(hrp2jsknt_moveit_demos)

find_package(catkin REQUIRED COMPONENTS
  ompl_rviz_viewer
  moveit_planners_ompl
  random_numbers
  moveit_core 
  moveit_ros_planning 
  moveit_ros_planning_interface 
  pluginlib
  moveit_visual_tools
  hrp2_moveit_msgs
)

find_package(Eigen REQUIRED)
find_package(Boost REQUIRED system filesystem date_time thread) # serialization)

catkin_package(
#  INCLUDE_DIRS include
  CATKIN_DEPENDS
    ompl_rviz_viewer
    moveit_planners_ompl
    random_numbers
    moveit_core
    moveit_ros_planning_interface
    moveit_msgs
    interactive_markers
    moveit_visual_tools
)

###########
## Build ##
###########
include_directories(SYSTEM ${Boost_INCLUDE_DIR} ${EIGEN_INCLUDE_DIRS})
include_directories(${catkin_INCLUDE_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

add_executable(hrp2_demos src/hrp2_demos.cpp)
target_link_libraries(hrp2_demos ${catkin_LIBRARIES} ${Boost_LIBRARIES})
add_dependencies(hrp2_demos hrp2_moveit_msgs_gencpp ${PROJECT_NAME}_gencfg) # wait for external msgs to be built

add_executable(random_poses_grounded src/random_poses_grounded.cpp)
target_link_libraries(random_poses_grounded ${catkin_LIBRARIES} ${Boost_LIBRARIES})
add_dependencies(random_poses_grounded hrp2_moveit_msgs_gencpp ${PROJECT_NAME}_gencfg) # wait for external msgs to be built