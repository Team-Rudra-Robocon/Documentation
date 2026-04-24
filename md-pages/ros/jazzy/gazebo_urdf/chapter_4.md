# Broadcasting TF with a publisher
<sub>**Author**
Isha Erande</sub>
-- connecting ros with urdf files --

We have a URDF file , 
1. start the /robot\_state\_publisher node  
2. We need to pass this urdf file as a parameter to the /robot\_state\_publisher node , 
3. The node also needs the state of joints given by the /joint\_states topic 
4. The publisher then compute the TF and publish on the /tf topic
5. This /tf topic will be used by other nodes.

### What is a launch file ?
 a launch file is basically a file which when executed , it runs multiple programs / set of commands at once , without the need to run many commands manually on terminal , 
 
 in ROS2 , the launch file launches the whole set of files like urdf , rviz and even the nodes which are connected to the urdf which help in motion of the robot.
launch files can be of 2 types : a python file or an xml file , 
ROS1 always worked on XML while python launch file was implemented in ros2 , and that's is most commonly used today , 

Note: you can create a python launch file in xml as well.

eg. of an xml launch file:
~~~

<launch>
    <let name="urdf_path"
     value="$(find-pkg-share my_robot_description)/urdf/my_robot.urdf" />

    <node pkg="robot_state_publisher" exec="robot_state_publisher">
        <param name="robot_description"
        value="$(command 'xacro $(var urdf_path)')" />
    </node>

    <node pkg="joint_state_publisher_gui" exec="joint_state_publisher_gui" />

    <node pkg="rviz2" exec="rviz2" output="screen" />
</launch>

~~~

here the launch file executes the 3 nodes together at once.

Steps to the above:

1. make a ros2 package
2. create a launch file 
----- to add more --------
