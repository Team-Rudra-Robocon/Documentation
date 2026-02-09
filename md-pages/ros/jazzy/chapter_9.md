# ROS2 Topics
<sub>**Author**
Isha Erande</sub>

A topic is a critical section in OS, where a publisher publishes to the topic and a subscriber subscribes to a topic. Its like a shared space, therefore publisher and subscribers uses topics to publish and subscribe to information.

A topic can have many publishers and many subscribers. The subscribers receive msgs from all the publishers. This can be done by creating a node to publish and subscribe to it.


A publisher only publishes data, it doesn't know who the subscriber is and similarly the subscriber just takes data from the topic and doesn't know who published it to the topic.

Similarly a single publisher can publish to different topics as well.

A topic is used to send a data stream and it is unidirectional, there is no feedback.

A topic has a msg type and the pubs and subs should follow the msg type. This can be written in py, cpp ... directly inside the node.

This can help in separating the code and communicating using topics.

---
## Creating a Publisher

```
.create_publisher(msg_type , topic_name , 10) 
```
this function helps in creating a publisher and add the topic name to it  , the topic name is like the critical section , that helps in publishing the information

```
.publish(msg)
```

this helps in publishing the msg to the topic.

---
## Creating a Subscriber : 

```
.create_subscription(msg_type , topic_name , callback_function , 10)
```

this function creates a subscription to the topic mentioned , it even stored to data into a callback function which needs to be created inside the node itself, then it that data can be printed on the terminal using
``` getlogger().info() ```

---
### more about topics and how to debug topic using command line tools
1. ```ros2 topic``` : 
this can handle topics and it has many functionalities to debug it .

2. ```ros2 topic list```:this gets you the list of running topics.

3. ```ros2 topic info```: this gets you the information of the specified topic

4. ```ros2 topic echo (topic name)```: this creates the subscriber on the terminal itself to ensure that the data is publishing successfully.
5. ```ros2 topic hz (topic name)```: this gets you the avg rate and frequency of the running program.
6. ```ros2 topic pub -r 10 (topic name)```: rate of publishing 10hz here. eg.
say you have 2 publishers publishing at different rates , the receiver / subscriber will receive the data in that rate only , say one publisher is publishing at 10hz and other at 20 hz the publisher publishing at 20hz will send more data than 10hz publisher , this helps in having different publisher publish at different rates

---
## remapping a topic at runtime

like remapping a node we can also rename a topic at runtime 
```
ros2 run my_py_pkg robot_news_station --ros-args -r __node:=my_station
```
something like this , it remaps the node here , to do the same for topic we simply add another flag 

```
ros2 run my_py_pkg robot_new_station --ros-args -r __node:=my_station -r robot_news:=my_news

ros2 run my_py_pkg robot_news_subscriber --ros-args -r robot_news = my_news 
```
here robot_news is the hardcoded topic in my publisher and subscriber file , therefore the above command will check if there exist any "robotnews" , if it does then it will replace it with "mynews" , now if you check the subscription it will not receive anything as the topic name is changed , you also need to change the topic name for subscriber as well. Now the subs will start printing the data 

---
### Monitoring topics with rqt_graph

rqt graph gets you the visualised information about active topics , services or action servers.
~~~bash
rqt_graph
~~~

this gets you all the publisher , subscribers , servers clients etc active and interacting visualised in form of a graph.
