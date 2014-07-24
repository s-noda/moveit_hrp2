hrp2_moveit
===========

Workspace for MoveIt! manipulation integration with HRP2NT. Note that the HRP2 model (URDF) is private, so this repo is not useful unless you have access to hrp2jsknt_description.

## Install

To use this repo:

* Install wstool package if you have not already:
    ```
    sudo apt-get install python-wstool
    ```

* Create a catkin workspace

    ```
    mkdir -p ~/ros/ws_hrp2/src
    cd ~/ros/ws_hrp2/src/
    catkin_init_workspace
    ```

* Use the rosinstall file to pull in all necessary repositories.
  This includes various repos as needed to build at the time of this writing (based on what is available as debians)

    ```
    wstool init .
    wstool merge https://raw.githubusercontent.com/davetcoleman/moveit_hrp2/master/moveit_hrp2.rosinstall
    wstool update
    ```

* Add the private package hrp2jstnt_description if you have access (sorry).

* Install dependencies
    ```
    rosdep install --from-paths src --ignore-src --rosdistro hydro -y -r
    ```
    *This may not work well if you have rosbuild/pre-Hydro packages in your repository

* Build the workspace
  
    ```
    cd ~/ros/ws_hrp2/
    catkin_make
    ```

* Build necessary ROS messages into LISP version
    ```
    rosrun roseus generate-all-msg-srv.sh moveit_msgs sensor_msgs geometry_msgs trajectory_msgs std_msgs actionlib_msgs visual_msgs std_srvs hrp2_moveit_msgs jsk_ik_server cmake_modules
    ```

* Only if you have issues - try installing these other Ubuntu dependencies (required by jsk-ros-pkg, not this repo)
    ```	  
    sudo apt-get install -y libomniorb4-dev omniidl libomniorb4* omni* libblas* liblapack* f2c omniidl-python omniorb-nameserver libomniorb4-1-dbg libomniorb4-dev omniorb omniorb-idl python-omniorb-dbg python-omniorb-doc
    sudo apt-get install -y gsfonts-x11 texlive-fonts-extra xfonts-100dpi xfonts-75dpi xfonts-100dpi-transcoded xfonts-75dpi-transcoded
    sudo apt-get install -y openjdk-7-jre openjdk-7-jdk 
    sudo apt-get install -y ros-hydro-ps3joy ros-hydro-rosjava-build-tools drcsim-hydro ros-hydro-moveit-full ros-hydro-actionlib-tutorials    
    ```
  
## Instructions

Launch Rviz
```
roslaunch hrp2jsknt_moveit_config moveit_rviz.launch 
```

Launch the random pose generator test:
```
roslaunch hrp2jsknt_moveit_config random_poses_grounded.launch
```

You should now see the robot randomly generating poses in Rviz