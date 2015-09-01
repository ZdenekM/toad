cmake_minimum_required(VERSION 2.8.3)
project(toad_navigation_local)

find_package(catkin REQUIRED COMPONENTS roslaunch move_base)

catkin_package()

include_directories(
  ${catkin_INCLUDE_DIRS}
)

roslaunch_add_file_check(launch)
