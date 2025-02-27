# Chapter 5 : ROS2 Libraries and more about ros2 
<sub>**Author**
Isha Erande</sub>


we use rclpy for ros2 
its a ros2 library , also called ros client library , its handled purely in c and it helps in host to client library and its the base library as it is in c we need rclpy which is built on top of RCL library. The client library in built on top on rcl library , therefore any languages can have a client library like rclcpp , rcljs etc etc.

ros2 cli has many commands

```
ros2 run
```
 This command expect you to have a package and an executable <br> eg: 
```
ros2 run myRobotController myFirstNode
```
here myRobotController is the package and myFirstNode is the executable , 

if we need to launch a package , the package needs to be installed and should be concol build , the executables can be seen inside the package , PS: Ros2 also has its inbuild packages and executables 

you can use -h to see how the command is used 

```
ros2 node info/list
```
this gets you the nodes that are currently running with the list and the info to that node , it also gets you info abt the publisher and subscriber , rosout is oneof the publisher that helps you output the logger function to print the things on the terminal 

```
ros2 pkg create 
ros2 run
ros2 node list
ros2 node info 
```
source is important



