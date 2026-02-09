# Testing MoveIt
<sub>**Author**  
Isha Erande</sub>


A launch file is default provided by moveit when we configure it , use that launch file to check if everything is working or not. 

---
### Changes to make before using the launch file
1. Inside moveit_controllers.yaml , add 2 lines inside each group
   
    Before:

        <joint_name>_controller:
            type: FollowJointTrajectory
            joints:
            - Joint1
            - Joint2
            .
            .
            - JointN


    After:

        <joint_name>_controller:
            type: FollowJointTrajectory
            joints:
            - Joint1
            - Joint2
            .
            .
            - JointN
            action_ns: follow_joint_trajectory
            default: true



2. Inside the Joint limits , ensure all the limits are "True" by default and have a floating value if not change it likewise
   
            1 -> 1.0
            0 -> 0.0
            False -> True

---

### Launch the MoveIt demo to test the configuration

Use the following command to launch:
~~~bash
ros2 launch <robot_name>_moveit_config demo.launch.py
~~~