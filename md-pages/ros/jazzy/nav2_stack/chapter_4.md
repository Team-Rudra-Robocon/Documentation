# Using the generated map to navigate 

<sub>**Author**
Isha Erande</sub>


1. use the robot to open in the world first 
   
        ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py 

2. Use the following command to navigate


        ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=<path/map_name.yaml> 


    The above command will open rviz which will have a global map of the world , 

3. Add a 2D estimate:

    we need a 2D estimate to give the estimated start point , the estimated start point will basically tell where the robot is currently in the real world and what its local map looks like 

    Choose the "Add 2D estimate" and then choose the 2D estimate the estimates also needs you to add direction to the 2D estimate for estimated direction. 

4. choose goal 

    The goal is then set using the "set goal" option , you can set the navigation goal and watch the robot move acordingly to the goal , similarly we can add waypoints to make it move iteratively over the points provided.
