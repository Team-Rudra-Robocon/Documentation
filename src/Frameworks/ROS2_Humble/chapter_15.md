# Chapter 15 - URDF
<sub>**Author**
Isha Erande</sub>
 
 URDF : Unified Robot Discription Format

- it a file that describles all the functions and elements of the robot.
- its used to generate Tfs
- its in XML 

Note: To visualise the URDF file we use RViz.

the main part is to assemble 2 parts of a robot with a joint.

The whole file is in XML format which contains tags to create a link and a joint. Each link n joints have parameters and they work accordingly , The TF is defined in a Joint which connects two links together.

To find more info about the types of joints n tags , you can chekout [This link](https://wiki.ros.org/urdf/XML)
~~~
<?xml version="1.0"?>
<robot name="my_robot"> 
<!-- everything we write is in here , the robot functionality goes in here -->
    <material name="green">
        <color rgba="0 1 0 1" />
    </material>
    <material name="blue">
        <color rgba="0 0 1 1" />
    </material>

    <material name="grey">
        <color rgba="0.5 0.5 0.5 1" />
    </material>
    <link name="base_link">
        <visual>
        <!-- tells you how the whole link will look like  -->

            <geometry>
            <!-- the geometry of the link goes here -->
                <box size="0.6 0.4 0.2" /> <!-- here the size in in metric system with length width hight parameters in meters-->

            </geometry>
            <origin xyz="0 0 0.1" rpy ="0 0 0" /> 
            <material name="blue" />
        </visual>
    </link>

    <joint name="base_seond_joint" type = "revolute">
        <!-- the parent n child is the type of relation bet them and the origin defines the origin  of TF , axis tag only used when joint type is revolute , where a limit is added for rotation -->
        <parent link="base_link" />
        <child link ="second_link" />
        <origin xyz="0 0 0.2" rpy="0 0 0" />
        <axis xyz="0 0 1" />
        <limit lower="-1.57" upper="1.57" velocity="100" effort="100" />
    </joint>

    <link name="second_link">
    <visual>
        <geometry>
            <cylinder radius="0.1" length="0.2"/>
        </geometry>
        <origin xyz="0 0 0.1" rpy="0 0 0" />
        <material name="grey" />
    </visual>
    </link>

    <joint name="second_third_joint" type ="prismatic">
        <parent link="second_link" />
        <child link="third_link" />
        <origin xyz="0 0 0.2" rpy="0 0 0" />
        <axis xyz="1 0 0" />
        <limit lower="0.0" upper="0.6" velocity="100" effort="100" />
    
    </joint>

    <link name="third_link">
        <visual>
        <!-- tells you how the whole link will look like  -->

            <geometry>
            <!-- the geometry of the link goes here -->
                <box size="0.1 0.1 0.1" /> <!-- here the size in in metric system with length width hight parameters in meters-->

            </geometry>
            <origin xyz="0 0 0.05" rpy ="0 0 0.785" /> 
            <material name="green" />
        </visual>
    </link>

    


</robot>
~~~

This is an example .urdf file which has 3 links and 2 joints.

### Types of Joints

1. Fixed - all degrees of freedom locked , just a connection bet two links.
2. Revolute - it rotates around an Axis.
3. Continuous - its basically revolute but without limit , ie when wheels are moving for locomotion.
4. Prismatic - sliding joint , basically moves along an axis.

These are the most common joints.

### How to add a wheel ? 




