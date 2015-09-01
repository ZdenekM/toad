cmake_minimum_required(VERSION 2.8.3)
project(toad_gazebo)

find_package(catkin REQUIRED COMPONENTS roslaunch gazebo_ros gazebo_plugins gazebo_msgs hector_gazebo_plugins)

catkin_package()

include_directories(
  ${catkin_INCLUDE_DIRS}
)

roslaunch_add_file_check(launch)
