# Installation
<sub>**Author**
Isha Erande</sub>

~~~
sudo apt update
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-turtlebot3*
~~~

after the installation of Turtlebot3 there is a need to change the ./bashrc file.

~~~ python
 export TURTLEBOT3_MODEL=waffle
~~~

 For many of the new updates for Jazzy Jalisco , ROS LTS is still being built , therefore there may be a case where the installation commands dont work , if thats the case

 For GAZEBO Harmonic compatible with Jazzy Jalisco Distro , the installation should be done manually and not by using the default ros2 distro , use the documentation page for gazebo and nav2 installation. 


### Links for official installation are provided below:

[ROS2 Jazzy Jalisco](https://docs.ros.org/en/jazzy/Installation.html)
<br>
[Nav2 for Jazzy](https://docs.nav2.org/getting_started/index.html#installation)
<br>
[Gazebo Harmonic](https://gazebosim.org/docs/harmonic/install/)