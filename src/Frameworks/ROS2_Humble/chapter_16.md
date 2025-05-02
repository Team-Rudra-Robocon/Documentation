# Chapter 16 - Broadcasting TF with a publisher
<sub>**Author**
Isha Erande</sub>
-- connecting ros with urdf files --

We have a URDF file , 
1. start the /robot\_state\_publisher node  
2. We need to pass this urdf file as a parameter to the /robot\_state\_publisher node , 
3. The node also needs the state of joints given by the /joint\_states topic 
4. The publisher then compute the TF and publish on the /tf topic
5. This /tf topic will be used by other nodes.



Steps to the above:

1. make a ros2 package

----- to add more --------
