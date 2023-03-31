
### Table of contents
1. [Topic 2.1  What is JavaScript? ](#paragraph1)
2. [Topic 2.2  How do you use it? How do you debug?](#paragraph2)
3. [Topic 2.3  Basic setup of Vue.js framework ](#paragraph3)
4. [Topic 2.4  Practice!](#paragraph4)
5. [Questions](#paragraph)


# Unit 2:   Setting up our development environment (Part 2)

**- Summary -**
 
This unit is a general idea about **Javascript**. 

We'll set up a JavaScript framework, **Vue.js**, and define a standard to **debug the code** we are going to create throughout the course.


<p align="center"><b>
Step 1 : Environment preparation 
</b></p>
 

Let's prepare the environment for this **Unit 02**, create a new folder for it..

First, make sure you have **stopped the webserver** we started in the previous chapter. 
Go to the shell where you executed the command 
```
$ python -m SimpleHTTPServer 7000 
```
and press `Ctrl + c`


Create a new folder: **webpage_ws/unit_02**. Enter the folder and execute the web server from there.
```
$ mkdir ~/webpage_ws/unit_02
$ cd ~/webpage_ws/unit_02
$ python -m SimpleHTTPServer 7000
Serving HTTP on 0.0.0.0 port 7000 ...
```

Copy the **index.html** file from the previous unit to this new folder:

```
cp ~/webpage_ws/unit_01/index.html ~/webpage_ws/unit_02/index.html
```

 
## Topic 2.1   What is JavaScript ?  <a name="paragraph1"></a>

* JavaScript is a language created to help develop dynamic web pages.
* Dynamic web pages are the ones that **interact with user actions, updating the content, showing animations, or reacting to user data**. 

For reference about web and JavaScript foundations : https://developer.mozilla.org/en-US/docs/Learn/JavaScript

Web page contains HTML and can have CSS to add some style.  Now, to make things more interesting, we are going to add JavaScript to it.

* This programming language can **interact with external services, like APIs** through **assynchronous requests or websocket servers**.


## Topic 2.2 How do you use it ? How do you debug?  <a name="paragraph2"></a>


In our web page, let's add a new tag inside the **head** tag, just below the bootstrap library. Copy and paste the code below:

```html
<script type="text/javascript">
    console.log("Hello from JavaScript")
</script>
```

**Example :** 

```html
<head>
    <title>My first web page for ROS!</title>
    <script
    <link  href="https://stackpath.bootstrapcdn.com/  crossorigin="anonymous">
    <script type="text/javascript">
        console.log("Hello from JavaScript")
    </script>
</head>
```

Now, if you reload the page, nothing seems to be different. So, **what are we doing here?**

There is a very important tool we will use along the course, and it's called **Developer Tools (DevTools)**.
Throughout the course, it will be shown features provided by **Google Chrome browser**, but similar tools are present on **Mozilla Firefox**.



<p align="center"><b>
Step 2 : - Debugging the tab inside the course page -
</b></p>


## Topic 2.3 Basic setup of Vue.js framework  <a name="paragraph3"></a>



**What did we do there?**

Basically, the values from our **Vue object**, from the **main.js** file, are going to fill the places **{{ menu_title }}** and **{{ main_title }}**. 



## Topic 2.4 Practice! <a name="paragraph4"></a>

Let's practice a bit more using VUE to change the content on the web page.


Change the two paragraphs we have **`(<p>)`** and make their content come from the javascript file, like we did for the subtitles.






