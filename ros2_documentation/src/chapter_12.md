# Chapter 12 - ROS2 Parameters 
### What is ROS2 parameter ? 
 say you have a program that has a camera(Terminal Driver Node) node which have some variables like Name of USB device , FPS or if you want it to run from simulation mode , to change this we need to change the hardcode and do it again and again . but what if we need to run it 2 time with different times, this is wny hardcoding is not permitted , therefore this is where the parameters comes into picture. parameters are the configuration value that we can change during runtime .
 Therfore we need to declare the parameters inside the nodes and those values can be defined during runtime , now this helps us to start a node with different configuration as we provide the value during runtime. A parameter is specific to a node and is alive only when the node is alive. 2 different nodes have different parameters , a parameter has a name and a datatype , it can be anything .

### Declaring the parameters within a node 

we can work with parameters within terminal using 
```
ros2 param
```
this is how the parameters are seen from terminal.

```
ros2 param get
```
this gets you the value of parameters.

### how to declare the parameter . 
 inside the node we declate the parameter inside the consructor , with the parameter name . we can set a default value of parameter as well  
```
declare_paramters("<parameter_name>", <default_param>)
```
To sent a value of the parameter we need to declale it and then set the value , the value can be set using "ros2 param" command line tool
```
ros2 run <pkg_name> <node_name> --ros-args -p <param_name>:= value -p <param_name>:=value
```
we dont actually set the type , it is dynamically set as in we can set it to string at one point and then int during another runtime , therefore we can declare as many parameters as we want. 

### how to get and use parameters inside the node 
1. Declate parameter
2. use another function called
```
get_parameter(<param_name>).value
```
this gets you the parameter object then use that obj to get the obj.
 
3. for providing parameters in terminal we use the "ros2 run -p" command provided above 
