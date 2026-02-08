# Basics / Introduction

<sub>**Author**  
Isha Erande</sub>
Testing
testing
As this is a plugin inside ROS , we don't need to install a separate package or a separate executable file for it , use the following commands to install it . 

Note: This requires you to have ROS2 installed and setup according to the UBUNTU distribution.

~~~
sudo apt install ros-<distribution>-moveit
sudo apt install ros-jazzy-moveit
~~~ 

Note: To run moveit without lags or without delays and noise smoothly , we need a middleware which can interact easily with the nodes.

For jazzy its recommended to use Cyclone DDS , we need to install and export it 

1. Install it using the following: `sudo apt install ros-$ROS-DISTRO-rmw-cyclonedds-cpp`
2. As mentioned above its needs to be exported every time therefore recommended to change the ~/.bashrc file to export it automatically when the terminal is opened. 
   1. open `~/.bashrc` using nano(can use any text editor) -> `nano ~/.bashrc`
   2. Navigate at the bottom
   3. add the following line at the end before ros2 has been exported-> `export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp` 
   4. save the file using `CTRL+O , ENTER` then `CTRL-X`.

   
   set of commands 
ros2 run tf2_ros tf2_echo base_link left_gripper_link -> to know the absolute position of the end effector.

ros2 control list_controllers -> to know which controllers are active , and working 

