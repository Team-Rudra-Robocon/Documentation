# Requirements

<sub>**Author**  
Isha Erande</sub>

__Note: The course I followed was intended for a robotic arm with 6 degrees of freedom , but this can be done using any robot that u have built.__

Moveit Cannot directly be used on hardware , it needs to be configured on software before shifting to hardware. Therefore to use moveit we need a robot or at least a simulation of robot. Robot can be simulated using URDF and a simulation software like Gazebo or IsaacSim etc. Therefore look at my [ROS2-Gazebo/urdf](../gazebo_urdf/index.md) or the official [ROS2-GAZEBO](https://docs.ros.org/en/jazzy/Tutorials/Intermediate/URDF/URDF-Main.html) documentation to actually build and visualise a robot.

Moveit requires the robot to have moving joints and collision tags with inertia to help it plan better paths for the same. The urdf built can have a xacro format for better built or can still be a simple urdf. It should consist of a base link without the inertial tags but should consist of collision tags. 

The URDF that you build will be linked with moveit always therefore any changes you make will reflect in the moveit config.

