# Creating a YAML file to hold nav2 parameters 

<sub>**Author**
Isha Erande</sub>



# Working 


1. YAML files are one of the most effective ways to store parameters for a certain framework. You can create a YAML file to store information about existing motors , or information related to current state or home positions etc 
2. Similarly we can also store information about NAV2 parameters like which planner to use , what parameters does that planner need etc. 
3. Visit the official [nav2 documentation](https://docs.nav2.org/configuration/index.html#controller-plugins) to know more about the different planners in nav2.
4. Each planner has its own set of configurations , use the official [nav2 docs](https://docs.nav2.org/configuration/packages/configuring-controller-server.html#parameters) to set controller parameters.
5. Nav2 required to start a controller server, use the following command to start the controller server : `ros2 run nav2_controller controller_server --ros-args --params-file /home/path/to/your_yaml_file.yaml`
6. Activate the action node : `ros2 run nav2_util lifecycle_bringup controller_server`
7. This creates starts and activates an Action server , use that server to publish the plan or whatever feedback the planner requires using your custom node.
8. For example you can work on the inbuilt turtlebot waffle model , which has a camera and can be used for planning and navigation. There are other turtlebot models like "burger". Each with a different set of sensors and actuators , This can be combined with gazebo-ignition to get a simulation based planner.


# Debugging

1. `ros2 param list /controller_server` : Dumps everything the server knows about the controller and its parameters.
2. `ros2 launch nav2_bringup navigation_launch.py params_file:=/home/path/to/nav2_params.yaml` : explicitly tells the navigation launch file to look at exactly your parameters and not the default one.
3. `ros2 param get /controller_server FollowPath.max_linear_vel` : gives the value for that exact parameter, here FollowPath is a parameter , which has "max_linear_vel" as a parameter to set , therefore it will check if the changes are being updated.
