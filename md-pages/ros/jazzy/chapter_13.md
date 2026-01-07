# ROS2 Actions
<sub>**Author**
Isha Erande</sub>


Actions are communication types used for long running tasks 
They have 3 Parts (built on top of client - server architecture)

1. Goal 
2. feedback 
3. result 


Similar to services but actions can be canceled and provide feedback

an action client sends a goal to action server and when that goal is ack by the server it returns a stream of feedback as the result

## Why ?

the only communication types we have 

- ROS2 topic(Publisher Subscriber model)
- ROS2 services (Client server model)

We need good feedback not just a success and failure feedback which happens during services , 
plus we need something to cancel the execution 
we also need to handle multiple requests 

therefore Actions give us all of this and can

## Where ?

We use actions when we need longer services with feedback and cancellable execution.

~~~
Action Client                               Action Server
     |                                             |
     | -- Send Goal (move to x) (Service) -------> |
     |                                             |
     | <------ Accept / Reject ------------------- |
     |                                             |
     | -- Request Result (Service) --------------> |
     |                                             |
     | <------------Resopnse Result -------------- |
     |                                             |
     | <--------- Feedback (Topic) --------------- |
     |                                             |
     | -- Cancel Request(Service) ---------------> |
     |                                             |
     | <-------- Cancel Response ----------------- |
     |                                             |
     | <--------- Goal Status(Topic) ------------- |
     |                                             |
~~~

To Note: we can only have 1 server and multiple clients , if the goal interfaces it is in the server how the goals are handled


The action client and server you might know is turtlesim and turtle teleop key 

## Action commands

1. `ros2 action list` - gets list of active actions
2. `ros2 action list -t` - list of actions and their types
3. `ros2 action type <action_name>` - returns the type of a specific action
4. `ros2 action info <action_name>` - gives information about the action , like number of clients and servers active
5. `ros2 interface show <action_name>` - shows what exactly is there in the action





## Tempelate of a general ROS2 action:

~~~

#goal
datatype variable
---
# feedback 
datatype variable
---
# result
datatype variable

~~~
