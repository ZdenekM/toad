cmake_minimum_required(VERSION 2.8.3)
project(toad_stereo)

find_package(catkin REQUIRED COMPONENTS roslaunch stereo_image_proc sensor_msgs dynamic_reconfigure pluginlib)

catkin_package()

include_directories(
  ${catkin_INCLUDE_DIRS}
)

roslaunch_add_file_check(launch)
