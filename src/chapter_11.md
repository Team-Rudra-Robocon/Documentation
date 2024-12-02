# Chapter 11 - ROS2 interfaces - messages and services

## Ros2 Interfaces : 
ros2 interfaces are the packages which store the msg and srv which are used during publishing/subscribing to a topic or creating a service with a specific service type

```
ros2 interfaces show example_interfaces
```
the example_interfaces is a package inbuilt in ros that shows has its own msgs and services init . We can technically create msgs/services inside any pksgs , but its a good practice to keep your msgs/service defination in a single different package , where there is no code just msgs/service defination.

### ROS2 msg:
messages in ROS2 are certain type of information which are published to a topic. the information that we send to the topic are called msgs , therefore that msgs should have a type , the msgs type is what we can change using ros2 msgs. When we create a pulisher we need to specify the msg type as one of the arguements , that msgs type we can customize using ros2 msgs. 
Steps to create the msgs defination for a custom msg type:
1. create a pkg for msg/service
```
ros2 pkg create (pkg_name_interfaces)
```
no build type and no dependancies

2. now that the build type isnt specifies the file is created in cpp package , therefore remove include and source folder and then create a msg directory inside the pkg.
3. before building the msgs , we need to configure the type using cMake and package.xml file .
4. inside the package.xml file , we need to add new depend lines below the buildtool depend line :
```
<build_depend>rosidl_default_generators</build_depend> 
<exec_depend>rosidl_default_runtime</exec_depend>
<member_of_group>rosidl_interface_packages</member_of_group>
```
this helps in building 
5. Add one line in cmake file as well CMakeLists.txt file under findpackage
```
find_package(rosidl_default_generators REQUIRED)
```
6. Now we create a msg in the msg directory, create a new file with .msg extention , as a practice always name the msgs/services without the underscores.
7. inside the .msg file type the datatype and variable name, eg: 
```
int64 temperature
bool are_motors_ready
string debug_msg
```
 and then save this 
8. Then we need to add the sourcecode in CMake.txt file after the findpackage command :
```
rosidl_generate_interfaces({$PROJECT_NAME}
"msg/<name_of_msg_file.msg>"
)

ament_export_dependancies(rosidl_default_runtime)
```
we also need to add the export line inside 
9. then compile and colcon build that package then finally we have finally defined the msg type , now we need to add this msg inside a node to use it. 

we then include the node inside the node oyu want to create publisher/subscriber in

### ROS2 service 
 Similar to ROS2 packages , the ROS2 service is used for server/client communication. 
1. To create a custom srv defination we first need to create a directory inside the package , called "srv"
2. Then create the file with extention .srv inside that srv folder , edit the file .srv file with the request and respnce. eg:
```
float64 length
float64 width
"---" # this creates a gap between only the dashes
float64 area
```
inside the interfaces in cMake file add .srv file and add new line insdie it.
3. then directly build it then the service is ready.use this inside the service type by imprting it .


### Debugging msgs and Srv with command line(terminal)
```
ros2 interface show
```
helps you see the data inside the msg/ service 

```
ros2 interface list
```
this gets you all the interfaces we have .

```
ros2 interface package <pkg_name>
```
this gets you list of all the interfaces with that package

