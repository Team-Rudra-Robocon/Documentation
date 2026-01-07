# Moving robot in a simulated environment and generating a map
<sub>**Author**
Isha Erande</sub>
##  STEPS

1. start world: 
  The following command launches the robot inside the world   

        
        ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
        

2. start teleop keyboard to move the robot manually inside the world : This command opens an teleop interface to communicate to the simulated world

        
        ros2 run turtlebot3_teleop teleop_keyboard 
        
   
3. Launch Rviz to visualise the local map / lidar readings: It helps in visualising the map and visualising the local reading ie only the ones te lidar is able to see

    ros2 run nav2_map_server map_saver_cli -f nav2_maps/my_map
        ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
        
4. Save the map using the following:

      1. create a directory : ```mkdir <directory_name> ```
      2. Save the map using the following command : ``` ros2 run nav2_map_server map_saver_cli -f <directory_name>/<map_name>```


## Why ? 

You need to move the robot around the whole map to generate its map where the lidar will scan each and every point in the system and save it in a ".map" file which is nothing just a picture of how the objects / obstruction is placed. This is why the robot needs to move manually (linear and angular velocity). You can visualise the map from rViz.

## What does the map contain ?

The map directory contains mainly 2 files 

   1. [map_name].yaml  : This contains the metadata
   2.  [map_name].pgm : This contains the image
