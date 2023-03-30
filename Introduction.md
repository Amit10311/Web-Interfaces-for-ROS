## Unit 0:   Introduction to the Course

This unit is an introduction to the **Developing Web Interfaces for ROS** course. 

### What's this course about?

Every company that builds a robot, creates a solution for existing robots, or even uses a commercial one for its own purposes,
needs an interface to operate it.


Due to this necessity, we decided to push on "how to develop interfaces for ROS." 
In fact, there are many (many!) different ways to do that. 
* You can just provide a custom RViz template for your solution. 
* Using the well-known RQT library to build interfaces as ROS packages. 

Further, you can develop your own application that connects to a ROS Core network and do it the way you prefer (desktop apps, Android/iOS apps, etc.).


Which is the best one?

I can't answer this question! It depends on:

* **Who are you developing for?**
* **Which OS does it have to work on?**
* **Which resources do you have available to develop/maintain the app?**

So.. how do we deal with that?

A **generic, highly customizable, well-known** and **powerful** solution!

Many technologies arose and fell, but pure **HTML** never stopped being used! 
It only evolved, from crude elements to stylized (with **CSS**) and, further, became more and more dynamic (thanks to **JavaScript**).

How to use the best of web technologies (HTML, CSS and JavaScript) to build interfaces for ROS using the WEB.

-------------------------------------------------------------------------------------------------------------------

### Demo 1.1 


**1. Start rosbridge server**

In a web shell (the shell #1, for instance), run the **rosbridge websocket server**.
We are making all the ROS meta data (nodes, topics, services, params, etc.) available to our web clients through a websocket server.

```
$ roslaunch course_web_dev_ros web.launch
```
#
**2. Get the ROSBridge address of the computer assigned to you**

Every time you open the academy, our platform assigns to you a different remote computer.
In order to connect to it through web pages, we need to know the ROSBridge server address. 
Go to web shell **#2** and execute the following:

```
$ rosbridge_address
```
Example 
```
wss://i-02131eed912e2497d.robotigniteacademy.com/6336074d-6041-4ed8-9368-754414639243/rosbridge/
```

# 
**3. Connect to Rosbridge using the form below**

Execute the cell below. You must have a web page generated there.

Click over it and press **Ctrl + Enter**

Paste the **ROSBridge server address** into the field **ROSBridge address**

Press the Connect button!

```html
%%HTML
<div style="width:100%;">
<iframe src="https://s3.eu-west-1.amazonaws.com/readme.theconstructsim.com/__others__/index.html" style="min-width:100%; height:800px; border:0" />
</div>
```











