# Initiation , creating a workspace
<sub>**Author**
Isha Erande</sub>


use python-colcon and install that , and then also use autocomplete for it
<b>inside create a src directory , where we can colcon build it </b>



create a workspace for ros2 
```
mkdir ros2_ws
cd ~/ros2_ws
mkdir src
```


use colcon for building the workspace and need to source it.

```
colcon build
```



__NOTE: NEVER EVER BUILD THE PROJECT INSIDE SRC, ALWAYS BUILD THE PROJECT IN THE WORKSPACE WHERE THERE EXISTS AN "src" FOLDER.__
