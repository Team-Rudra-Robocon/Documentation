# Setup Assistant

<sub>**Author**  
Isha Erande</sub>

Moveit comes with its own built-in packages , it includes a setup assistant , its a GUI helped to configure moveit , u basically start with a URDF and other parameters like moveit-groups , or virtual links or even the ROS2-Control etc can be configured using that Moveit setup assistant , this helps users by adding an abstraction layer and making it easier to code other stuff than the parameters , 

## Steps to open and configure the urdf

1. Ensure that the URDF is in a description package somewhere `<robot_name>_description/urdf/<robot_name>.urdf`
2. Assuming this description package is in a src folder of a workspace , create another directory , usually its named something like this : `<robot_name>_moveit_config` this easily tells us where the file is located 
3. In the src folder itself , open the terminal and run the following command: `ros2 launch moveit_setup_assistant setup_assistant.launch.py` , auto complete can be used to actually launch this command. 
4. The assistant requires a urdf file if you are creating a new package , provide it the robot's URDF file using the folder structure mentioned above or wherever it might be. else directly choose the moveit_config package that already exist.
5. This will load other set of moveit parameters , go through each of the params now:
   1. __Self Collisions__: This tab generates a collision matrix of all the links present in the urdf , if some of the joints are not present in the real robot you might want to enable or disable  the collisions accordingly , use the UI and generate a collision matrix.
   2. __Virtual Joints__: These joints connect to the world / virtual world , therefore create a virtual joint that links the base link to the world.
   3. __Planning Groups__: Each of the robot joints can have a planning group of its own , for the purpose each arm can have a planning group of its own , The planning group consist of joints which need to be moved together in order for the arm to move to a specific place, therefore each planning group has an end effector , where they can know what the target should be. Use the add Group to add a Plannign group , or if there is an existing group , use the edit button to edit the joints and link from the group. Its very helpful while planning the path through cpp or python node. As this is where the final Kinematics solver looks to know which joints to move or even the plan is possible or not.The groups need a kinematics solver , if you have a different solver then add it manually after the configuration else just use the kinematics solver default in the pop-down options.
   4. __Robot Poses__: This part is where you can configure if you want to save a robot pose , orientation or stuff like that. you can choose the joint angles to actually create a pose for the robot to go to. 
   5. __End Effector__: This is where all the kinematics and planning acts on , if there is no end effector the child link is considard as an end effector.
   6. __ros2_control URDF Modifications__: Modifications done to control hardware are done here , just click on "Add Interface" , to actually create an interface, other things will be done automatically. Command Interfacce and Stat interface can be configured according to your needs.
   7. __ros 2 controllers__: They need to be set as to control hardware , no need if you already have a hardware controller parameter there. Click on "AutoAddJointTrajectoryContrller" to add a ros2 control to the config.
   8. __Moveit Controllers__: Moveit Controllers are a necessity to actually configure the path, these controllers are used to follow a trajectory which is given by the planner group.
   9. __Perception__: If you have an additional perception pipeline use this to add that as well. if no then just choose no.
   10. __Launch File__: Auto creates launch files easy for us to debug and / or check the configurations made.
   11. __Author Information__: Need to put something in the valid format may it be fake.
   12. __Configuration Files__: Finally after everything has been setup , we need to generate a configuration file , the configuration file needs to be saved in a directory , we have already made a  <robot_name>_moveit_config directory , choose this to actually save the configuration. 
   13. Finally exit the setup assistant.
6.  When you check there are files generated in the moveit config , that files are used by the planner to generate a valid plan and execute it.