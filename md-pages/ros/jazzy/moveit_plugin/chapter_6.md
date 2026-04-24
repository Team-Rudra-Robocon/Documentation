# MoveIt using CPP
<sub>**Author**  
Isha Erande</sub>


There are many ways to use CPP to plan a motion plan.

1. Joint Goal -> give fixed position for each joint (Forward Kinematics) 
2. Pose Goal -> give pose(x,y,z coordinates , with orientation) values and the path is planned directly to the goal pose.(Inverse Kinematics)
3. Waypoint / Cartesian Goal -> give a set of points to go through to the end goal , this is used when the object needs to picked in a planned path or a different way than the regular , the coordinated create a waypoint of coordinated which the end effector has to follow in order to reach the end position with correct orientation.



Orientation Control : This keeps the orientation of the end effector to be fixed and without changing the end effector orientation , it plans a path accordingly , its a part of Cartesian Goal.

Robot Workspace : Moveit allows you to create a robot workspace as well ? use the moveit group for creating robot workspace `group.createWorkspace(x_min , y_min , z_min , x_max , y_max , z_max)` , for each group.
