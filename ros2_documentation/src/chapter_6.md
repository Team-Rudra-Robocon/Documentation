# Chapter 6 : colcon

colcon is a tool used for build in ros2

```
colcon build
```
it can have many arguements with it aswell , we have autocompletion as well. 
one issue wiht colcon build is , we need to build it everytime we update the program, therefore it can be made a lot faster 
### how can we work faster with it ?
```
colcon build --packages-select my_py_pkg --symlink-install
```
this will help you directly without needing to colcon build it again and again , symlink helps you do that , to use the symlinkinstall flag remember to make the file executable

