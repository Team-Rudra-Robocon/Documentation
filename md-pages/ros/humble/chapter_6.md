# colcon
<sub>**Author**
Isha Erande</sub>


colcon is a tool used for build in ros2

```
colcon build
```
it can have many arguments with it as well , we have autocompletion as well. 
one issue with colcon build is , we need to build it every time we update the program, therefore it can be made a lot faster 
### how can we work faster with it ?
```
colcon build --packages-select my_py_pkg --symlink-install
```
this will help you directly without needing to colcon build it again and again , symlink helps you do that , to use the symlink install flag remember to make the file executable
