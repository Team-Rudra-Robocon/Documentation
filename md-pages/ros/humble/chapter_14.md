# TF 
<sub>**Author**
Isha Erande</sub>

### What is TF ? 

TransFormations:
it basically an Axis , where a 3d axes is visualised , every link has a TF which relates to each other links , it gives each link an origin to locate itself from other links.It also helps in knowing how they move relative to each other , that is what TF does , it gives an origin to each link , which move relative to other links
TFs are basically joints like ur body they define how a robot moves using the rigid parts of the robots , and how they move relative to each other.

### What is TF Tree ?
The relationship between the Tfs is called the TF tree, it is visualised by arrows where the TF points to its parent TF. this is how each TF are defined and they become a tree which relate the TFs with each other , and gives it a relationship to move which respect to that. 

When a parent TF is moved all the corresponding TF children move too. but not vice versa.

The information about Tf is published on a TF topic , it can be accessed through the command like : 
~~~
ros2 topic list
~~~

check if '/tf' is visible then : 
~~~
ros2 topic echo /tf
~~~

The published info will be printed on the terminal itself.



### tool to visualise the TF tree 

tf.tools package is used to visualise the tf tree in ros2. The package is already installed but just in case :

install the package through: 
~~~
sudo apt install ros-jazzy-tf2-tools
~~~

Note: change the distro name according to your version.

to visualise run the following command 
~~~
ros2 run tf2\_tools view\_frames
~~~
this will listen to the tf topic for 5 seconds and then create a pdf file with TF tree.


### Why TF ? need for TF ??
1. Tf keeps a structured way of frames and joints , ie how frames are placed and how they move to each other. 
2. A transformation is basically a translation+ rotation , we take an obj , we move it and rotate it , for each frame we need to compute transformation for each frame which is complex therefore that's what TF does for you.
3. The URDF files helps keep and update TF.
