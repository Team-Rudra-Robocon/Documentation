# Chapter 4 : Creating a Node and ros2 packages

to create a node we need packages which help you saperate the block of codes eg. packages will saperate tasks of the robot 

To create packages we use 

```
ros2 pkg <pkg name> --build-type ament_python --dependencies rclpy 
```

rclpy is the module of python that has Ros2 

After creating a pkg inside src folder , we need to build it , using colcon build
```
colcon build
```
this is done every time a package is created and modefied


### what is ROS2 node ? 
its a subpart of package , nodes communicate with eachother ans is used to comunicate with each other , nodes are communicating with other packages as well.

Nodes can be written in any languages , ie one in cpp and other in python , and they stil can communicate with each other

Creating a node : 

we create a class and that class is your node , it needs a main() function and init and shutdown rclpy
we can create node by importing node from rclpy


### Running the node 

1. create executable and launch it 
2. colcon build it and then source it 
3. running using python3

<P>its better to use colcon to run the program ie : ros2 run myRobotController myFirstNode ie using ros2 to run it 
This has its own benifits 

installing it is by updating setup.py in the package

<P>To create a node using OOP we have class , make a class which inherits from node and use that object to access or run a node. There are timer callbacks as well which helps you run a certain code in a specific time interval like the way we write while(1) , but calling the function in a certain amt of time.

The spin() function in ros is basically a function that keeps the node alive untill forced to closed ie. keyboard interrupts

The main function will always have the same functions :
1. To create a node (node object)
2. spin the node or update it 
3. close the node using shutdown() function 

### Templete for a ros2 node 
```
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node
 
 
class MyCustomNode(Node): # MODIFY NAME
    def __init__(self):
        super().__init__("node_name") # MODIFY NAME
 
 
def main(args=None):
    rclpy.init(args=args)
    node = MyCustomNode() # MODIFY NAME
    rclpy.spin(node)
    rclpy.shutdown()
 
 
if __name__ == "__main__":
    main()
```

This is the basic templete refer this whenever needed.

### Renaming a node at runtime 

in ros2 you can rename the node say you have 5 lidar sensors then you need to run the same node 5 times , which is not a big issue but running nodes with same name can cause problems , therefore we require renaming it during runtime , it create communication problems and confusion , when you need to see information

how can you do so ??

we can use 

```
ros2 run <pkg_name> <executable_name> --ros-args --remap__node:abc
```

when we run this the node is reames to abc , and we can do that for each and every node and then use info with that runtime name to fine info for that soecific node.This feature is handy for duplication of nodes.

