# Inside MoveIt Config Package
<sub>**Author**  
Isha Erande</sub>


The setup assistant generates a Configuration Package , the package generated contains following directories and files:

~~~
<robot_name>_moveit_config
├── CMakeLists.txt
├── config
│   ├── industrial_robot.ros2_control.xacro
│   ├── industrial_robot.srdf
│   ├── industrial_robot.urdf.xacro
│   ├── initial_positions.yaml
│   ├── joint_limits.yaml
│   ├── kinematics.yaml
│   ├── moveit_controllers.yaml
│   ├── moveit.rviz
│   ├── pilz_cartesian_limits.yaml
│   └── ros2_controllers.yaml
├── launch
│   ├── demo.launch.py
│   ├── move_group.launch.py
│   ├── moveit_rviz.launch.py
│   ├── rsp.launch.py
│   ├── setup_assistant.launch.py
│   ├── spawn_controllers.launch.py
│   ├── static_virtual_joint_tfs.launch.py
│   └── warehouse_db.launch.py
└── package.xml
~~~

Each file contains specific configuration information about the robot which needs motion planning.

1. __CMakeLists.txt__ : Contains compilation information and tracking information
2. __config__: All the information about robot configuration is stored in this directory
    1. __[robot_name].ros2_control.xacro__ : This contains the ros2_control tags needed in the robot urdf , therefore , this is used for hardware control
    2. __[robot_name].srdf__ : This contains the collision , saved robot poses , links and joints, group information , end effector tag etc. etc. 
    3. __[robot_name].urdf.xacro__: copy of robot urdf
    4. __initial_positions.yaml__: saves the initial position of the joints , joints can have different initial positions than 0, this can help while initiating the robot.
    5. __joint_limits.yaml__ : Contains velocity and acceleration limits for each joint specified(uses ros2_control to know which joints are specified and used), make sure to keep all the limit explicitly a float or double so change any "1" -> "1.0" also by default keep everything as "True".
    6. __kinematics.yaml__ : Specified which kinematic model to be used for each group , if there are multiple it uses the first one specified. KDL by default.
    7. __moveit_controllers.yaml__ : This is the main controller moveit uses to plan motion , this contains all the joints in a single group and which joints are used here 
    8. __moveit.rviz__ : Visualisation information , where and how the robot should be when rviz is used
    9.  pilz_cartesian_limits.yaml
    10. __ros2_controllers.yaml__ : This file is used for hardware control 
3. __launch__ : All the launch file to launch all of the configuration together
    1. __demo.launch.py__ : used to check of moveit is configured correctly or not
    2. __move_group.launch.py__ : used when using cpp or python to run the robot with moveit
    3. moveit_rviz.launch.py
    4. rsp.launch.py
    5. setup_assistant.launch.py
    6. spawn_controllers.launch.py
    7. static_virtual_joint_tfs.launch.py
    8. warehouse_db.launch.py
4. __package.xml__ : dependencies and package information is stored here






