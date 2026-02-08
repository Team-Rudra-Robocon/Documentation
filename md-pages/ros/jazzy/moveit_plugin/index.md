
<sub>**Author**  
Isha Erande</sub>

# what is moveit ? 
   
   moveit is a motion planning plugin used along with ROS2. It contains all the information to plan a path of how an object is going to move.

   its usually used when multiple joints are connected in series to create a robot with multiple degrees of freedom , for a robot to go to any point in the robot workspace it needs to have at least 6 degrees of freedom. for example: Robotic Arms , which requires immense amount of Inverse and Forward Kinematics to work. As the joint increase the math behind IK and FK also increases , which is complex when most of the work is always away from that level of niche math, This plugin helps in planning and calculating FK and IK , so you don't have to.
   
   