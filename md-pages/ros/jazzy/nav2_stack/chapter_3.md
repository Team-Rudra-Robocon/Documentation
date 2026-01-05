# Moving robot in a simulated environment
<sub>**Author**
Isha Erande</sub>

### Start turtlesim in a simulated world 
~~~
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
~~~

The above command works for ROS2 distributions before Jazzy , for Jazzy as the Gazebo changes fom Gazebo Classic to Gazeboo Harmonic , the launching the world

~~~
ros2 launch nav2_bringup tb3_simulation_launch.py headless:=False
~~~

The above command launches the gazebo world with waffle and opens Rviz + Gazebo simulation.
Check the rqt graph for the nodes and topics that the inbuilt turtle bot has , use that to navigate from in the world.