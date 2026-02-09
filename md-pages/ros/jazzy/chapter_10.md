# ROS2 Service(Client and Server architecture)
<sub>**Author**
Isha Erande</sub>

services are used for a client and server interaction

say we have a weather service which is a server and provides you with weather info 
when loc is provided and you the client trying to access the weather using an http 
request ,

now what will happen is the client will send a request and the server accepts the 
requests and it must send back a proper response , therefore one client and one 
server can communicate with each other easily but say we have multiple clients , then 
the multiple client will send requests using the same http request , and then the 
server will process the request and then send the response to the client

eg. You have a node that controls led panel and that node should communicate to 
outside node , say you need to send a msg to the led node to turn on a LED when 
battery percentage is low , we can do so by creating a service setLED , then creating 
a server inside the LED node , and creating a client that will be the battery percent 
, when the battery percent is low , then the client will send a request/msg through 
the service to the server , msg being turning which light on , this msg is then 
processed and the light is turned on. Then the server will send a response to that 
client to notify that the request has been successfully performed , ie send a flag. 
The client is waiting synchronously or asynchronously for the response , now say you have 
a full battery , the battery node sends a request through the service to turn off the 
leds , then the same request is processed by the server and after processing a 
response or a flag is sent ensure the request has been processed.This is how the ros2 
service work ?

You can directly create a service using rcl library , and also it has a single server 
with many nodes for a single service. The service will exist when a server is created.

---
### Creating a server
1. A service is created inside the server node
 ``` node.create_service(typeOfService , 
serviceName , callBackFunctionForService)
 ```
the above line of code creates a service 
inside the server node , the callback function has the thing that you need to process 
or the request is processed in the callback function that contains 2 parameters , 
request and response where response is returned and request is processed. in adding two 
numbers example the request is the 2 numbers coming from clients and the response is 
the sum. therefore the callback function does the job of calculating the sum and 
returning the appropriate response.

---
### Creating a client
1. without using oop this method is used directly inside the main function without 
 using oop to create a node ie directly creating the node inside the main function.
```
 node.create_client(typeOfService , serviceName)
 ```
 This takes in 2 parameters , 
also it needs to wait for sometime for the request to process we add future

```
 client.call_async(request) 
```
 this function creates a future ie , waits for 
request to process

then rather that using .spin() function always we use
 ``` 
spin_until_future_complete(nodeName , future) 
```
 
to spin until the future is complete 
or the request is processed we store the requested response in a variable and then 
print it .

---
2. with oop what we do using OOP is we create a class inheriting from node like done 
 previously , and then what we do is we create a function inside the node that sends 
 out requests to the clients , that function creates a client and then adds requests
```
self.create_client() 
```
 
this create the client this is then used to send requests 
, an object of AddTwoInts.request() is created called as requests and then that stores 
the data to be sent to the server ie the 2 numbers. therefore similar to the future 
used in the not oop case we use future , but to see the response a callback is 
necessary therefore a callback function is attached to the future which will be called 
as soon as the response is sent. just like before the callback function does all the 
processing , here printing the response ie the sum.

the program without oop is easier and simpler to implement , but the program using 
oop is usually used in a file or a project , it is much more complex but it 
gives us.

---
### ROS2 client for cpp 

the issue with creating a client with oop is that , while calling the callback function inside the constructor the "future.get()" function will stop the execution and the the node will not spin therefore we need to call the callback service function on a new thread , for that you need to create new thread and use that for calling that function thereby letting the program execute

---
## How to debug Services using CLI / Terminal
``` 
ros2 service
 ```
 this gets you all the commands needed for debugging services

```
 ros2 service list ros2 service call
```
 
this helps in listing all the services and 
the call used to call the service using Terminal ig using the service on Terminal. 
This can be used to debug the service

```
 ros2 service type
 ```
 This gets you the type of service that is being 
processed(The first parameter from the create service function)

rclpy also helps in creating a client and using client service

---
## remap a service at runtime

just like nodes and topic we cna remap the services as well , similarly by using 
ros-args -r
