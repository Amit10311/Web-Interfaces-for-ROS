### Table of contents
1. [Topic 3.1  Lifecycle of the page](#paragraph1)
2. [Topic 3.2  Handling events of the page + Controlling the robot](#paragraph2)
3. [Topic 3.3  Practice](#paragraph3)
5. [Questions](#paragraph)


# Unit 3:   Move the Robot! Publishing to a topic!

**- Summary -**
 
In this unit, we'll **connect to ROSBridge**, as we have seen in the introduction, but now by creating our own code. 

* You will see step-by-step **how to configure your JavaScript code** to connect from a **Vue.js** application. 

* After that, we will publish to a **ROS topic** in order to move the robot in the simulation.


<p align="center"><b>
Step 1 : Environment preparation 
</b></p>
 

Let's prepare the environment for this **Unit 03**, create a new folder for it..

First, make sure you have **stopped the webserver** we started in the previous chapter. 

```
$ python -m SimpleHTTPServer 7000 
```
and press `Ctrl + c`


Create a new folder: **webpage_ws/unit_03**. Enter the folder and execute the web server from there.

```
$ mkdir ~/webpage_ws/unit_03
$ cd ~/webpage_ws/unit_03
$ python -m SimpleHTTPServer 7000
Serving HTTP on 0.0.0.0 port 7000 ...
```

Copy the **index.html** file from the previous unit to this new folder:

```
cp ~/webpage_ws/unit_02/* ~/webpage_ws/unit_03/
```
 
<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 3.1 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 3.1   Lifecycle of the page <a name="paragraph1"></a>

In our case, we have a **static web** page so far, but a **main.js** file that depends on the **HTML** content to do the magic of the framework.
That's why we appended the reference to such file at the end of the **body** element.

Something that comes out of the box, with **Vue.js**, is a method called **mounted**. 
This method is called whenever the page gets ready. Update your **main.js** file with the content:

```html
let vueApp = new Vue({
    el: "#vueApp",
    data: {
        menu_title: 'My menu title',
        main_title: 'Main title, from Vue!!',
    },
    mounted() {
        console.log('page is ready!')
    },
})
```

<p align="center"><b>
Step 2 :  Connecting to ROSBridge when page is loaded 
</b></p>

```
$ roslaunch course_web_dev_ros web.launch
```

```
$ rosbridge_address
wss://i-0d106dc13df6e5dee.robotigniteacademy.com/cefbda62-ce06-4845-8c38-1766f3c13b37/rosbridge/
```
```
$ webpage_address
https://i-0d106dc13df6e5dee.robotigniteacademy.com/cefbda62-ce06-4845-8c38-1766f3c13b37/webpage/
```

Let's prepare our **index.html** and **main.js** files to do such a connection.

**Step 1 :** Add the **roslib.js** library to our page. 
* Do this by adding a new script to the **head** section. 

```html
<head>
    <title>My first web page for ROS!</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.min.js"></script>
    <script src="https://static.robotwebtools.org/roslibjs/current/roslib.min.js"></script>
</head>
```

And the **main.js** will be improved a little bit:

(* Pay attention to the value of **rosbridge_address**. You must use the one you took from the terminal command!)

```js
let vueApp = new Vue({
    el: "#vueApp",
    data: {
        // ros connection
        ros: null,
        rosbridge_address: 'wss://i-0123456789.robotigniteacademy.com/rosbridge/', // change to your own address
        // page content
        menu_title: 'My menu title',
        main_title: 'Main title, from Vue!!',
    },
    mounted() {
        // page is ready
        console.log('page is ready!')

        // define ROSBridge connection object
        this.ros = new ROSLIB.Ros({
            url: this.rosbridge_address
        })

        // define callbacks
        this.ros.on('connection', () => {
            console.log('Connection to ROSBridge established!')
        })
        this.ros.on('error', (error) => {
            console.log('Something went wrong when trying to connect')
            console.log(error)
        })
        this.ros.on('close', () => {
            console.log('Connection to ROSBridge was closed!')
        })
    },
})
```

Pay attention to the value of **rosbridge_address**, it must be the address calculated on your web shell.
Try to reload the page.
* You must have the following results on your **Console** and **Network** tabs of the **DevTools**:

![image](https://user-images.githubusercontent.com/20908007/230382803-049fb1b3-eaed-4e86-872c-c0758d79a847.png)


It means you have reached the point of the connection! Check the next image.


![image](https://user-images.githubusercontent.com/20908007/230393457-f8332e1d-eb1a-4e7c-be4c-f439e2869cfd.png)


You can see we have a **websocket connection established** (Pay attention to the subtab WS).
If you click on the connection, you will see more details like the address and messages exchanged. 



<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 3.2 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 3.2  Handling events of the page + Controlling the robot<a name="paragraph2"></a>


We have a **Vue.js** web app connecting to our **ROSbridge Server**. 
Now, let's give more control to our web page. Let's do the following:

* Input the address through the page

* Create a button to connect or disconnect

* Create a button to send velocity commands to the robot in the simulation


Let's start from the **main.js** file. It will contain methods to handle all these **events**.


```js
let vueApp = new Vue({
    el: "#vueApp",
    data: {
        // ros connection
        ros: null,
        rosbridge_address: 'wss://i-0734dfc7411934198.robotigniteacademy.com/rosbridge/',
        connected: false,
        // page content
        menu_title: 'Connection',
        main_title: 'Main title, from Vue!!',
    },
    methods: {
        connect: function() {
            // define ROSBridge connection object
            this.ros = new ROSLIB.Ros({
                url: this.rosbridge_address
            })

            // define callbacks
            this.ros.on('connection', () => {
                this.connected = true
                console.log('Connection to ROSBridge established!')
            })
            this.ros.on('error', (error) => {
                console.log('Something went wrong when trying to connect')
                console.log(error)
            })
            this.ros.on('close', () => {
                this.connected = false
                console.log('Connection to ROSBridge was closed!')
            })
        },
        disconnect: function() {
            this.ros.close()
        },
        sendCommand: function() {
            let topic = new ROSLIB.Topic({
                ros: this.ros,
                name: '/cmd_vel',
                messageType: 'geometry_msgs/Twist'
            })
            let message = new ROSLIB.Message({
                linear: { x: 1, y: 0, z: 0, },
                angular: { x: 0, y: 0, z: 0.5, },
            })
            topic.publish(message)
        },
    },
    mounted() {
        // page is ready
        console.log('page is ready!')
    },
})
```

<p align="center"><b>
Code explanation 
</b></p>
 

In our **data** attribute, we are defining 3 new attributes: **ros, rosbridge_address, and connected**. 

* The first one will contain the connection handler to the rosbridge server. 
* The second stores the address of the rosbridge server. 
* Finally, the **connected** variable is a flag of the connection status.

# 

Next, we have something new about Vue.js, which is the **methods** attribute.
We can define functions inside this attribute, all of them, as the **data attribute** can be used inside the Vue app scope. 
The first method, **connect**, contains the instructions we put inside **mounted** previously.


Here we have some instructions that rely on **roslib.js**. We have the object installation `new ROSLIB.Ros`, that creates a connection. It's necessary to pass the parameters `url`.

Next, we define some **callbacks**. The connection to the `rosbridge server` is asynchronous. 
So, events like **connection, error**, and **close** must be handled like that: `ros.on("event_name"), () => {`. 

# 

The second method, **disconnect**, is quite simple and just closes the connection to the `rosbridge server`. 
It's important to notice here that the variable `this.ros` refers to the same this.ros we have worked with on the **connected** methods.
That's because the framework provides this scope between the methods.

The **topic** needs the following parameters:

* ros connection
* name of the topic
* type of the message

And the message itself must be a JavaScript object that contains exactly the same structure of ROS message. 

* You can check, for example, in a web shell the structure of **`geometry_msgs/Twist`**:

```
$ rosmsg show geometry_msgs/Twist
```

```py
 geometry_msgs/Vector3 linear
      float64 x
      float64 y
      float64 z
    geometry_msgs/Vector3 angular
      float64 x
      float64 y
      float64 z
```

Finally, we call the method **publish** of the object **topic**, passing the message as parameter.

<p align="center"><b>
 index.html
</b></p>

Now, let's finish the implementation in our **index.html** file. 

```html
<main id="vueApp">
    <div class="container">
        <div class="row">
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h3>{{ menu_title }}</h3>
                        <hr>
                        <label>ROSBridge address</label>
                        <br>
                        <input type="text" v-model="rosbridge_address" />
                        <br>
                        <button class="mt-2 btn btn-success" v-if="connected" @click="disconnect">Connected!</button>
                        <button class="mt-2 btn btn-primary" v-else @click="connect">Connect!</button>
                    </div>
                </div>
            </div>
            <div class="col-md-8">
                <div class="card">
                    <div class="card-body">
                        <h2 class="text-center">{{ main_title }}</h2>
                        <hr>
                        <p>Some actions for the robot</p>
                        <button class="mt-2 btn btn-primary" :disabled="!connected" @click="sendCommand">Move the robot!</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</main>
```

<p align="center"><b>
Code Explanation 
</b></p>
 












<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 3.3  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 3.3  Practice <a name="paragraph3"></a>














<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Questions %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Questions <a name="paragraph"></a>
















