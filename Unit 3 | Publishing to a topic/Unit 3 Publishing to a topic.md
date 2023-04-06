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

```html
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








<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 3.2 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 3.2  Handling events of the page + Controlling the robot<a name="paragraph2"></a>










<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 3.3  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 3.3  Practice <a name="paragraph3"></a>














<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Questions %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Questions <a name="paragraph"></a>
















