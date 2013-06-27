toad
====

ROS packages modified for our Toad outdoor robot based on Pioneer 3-AT platform


Dependencies:

* P2OS stack (https://github.com/ZdenekM/p2os)
* IMU/GPS driver (https://github.com/ZdenekM/microstrain_3dm_gx3_45)
* some Gazebo related stuff, please see README of toad_gazebo (https://github.com/robofit/toad/tree/master/toad_gazebo)
* anything else?

Installation instructions (for installing everything from scratch):

* create rosbuild workspace on top of catking workspace

```bash
source /opt/ros/groovy/setup.sh
mkdir ~/ros
mkdir -p ~/ros/catkin_ws/src
cd ~/ros/catkin_ws/src
catkin_init_workspace
cd ~/ros/catkin_ws
catkin_make
mkdir ~/ros/rosbuild_ws
cd ~/ros/rosbuild_ws
rosws init ./ ../catkin_ws/
source ~/ros/rosbuild_ws/setup.bash
```

* install standalone version of Gazebo

```bash
sudo apt-get remove ros-fuerte-simulator-gazebo ros-groovy-simulator-gazebo
sudo apt-get install build-essential libtinyxml-dev libtbb-dev libxml2-dev libqt4-dev pkg-config  libprotoc-dev libfreeimage-dev
sudo apt-get install libprotobuf-dev protobuf-compiler libboost-all-dev freeglut3-dev cmake libogre-dev libtar-dev
sudo apt-get install libcurl4-openssl-dev libcegui-mk2-dev

mkdir ~/devel
cd ~/devel
hg clone https://bitbucket.org/osrf/gazebo gazebo
cd gazebo
mkdir build
cd build
cmake ../
make -j5
sudo make_install
echo "source /usr/local/share/gazebo/setup.sh" >> ~/.bashrc
source ~/.bashrc
```

Now you should be able to run standalone Gazebo...

```bash
gazebo
```

* install catkin-based packages

```bash
cd ~/ros/catkin_ws/src
git clone https://github.com/ZdenekM/p2os.git
git clone https://github.com/osrf/gazebo_ros_pkgs.git
rosdep install --from-paths src --ignore-src --rosdistro groovy -y
cd ..
catkin_make
```

* install rosbuild-based packages

```bash
cd ~/ros/rosbuild_ws
rosws set microstrain_3dm_gx3_45 --git https://github.com/ZdenekM/microstrain_3dm_gx3_45.git
rosws update microstrain_3dm_gx3_45

rosws set hector_gazebo --git https://github.com/tu-darmstadt-ros-pkg/hector_gazebo.git
rosws update hector_gazebo

rosws set but_env_percp --git https://github.com/robofit/but_env_percp.git
rosws update but_env_percp

rosws set toad --git https://github.com/robofit/toad.git
rosws update toad

source ~/ros/rosbuild_ws/setup.bash

rosmake toad_bringup toad_gazebo
```

* make a small workaround

```bash
cp ~/rosbuild_ws/.........
```


* run simulation of our robot ;)

```bash
roslaunch toad_gazebo robot.launch
```


