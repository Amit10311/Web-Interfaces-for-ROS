# Unit 1:   Setting up our development environment (Part 1)

**- Summary -**
 
This unit is a general idea about web development.
We'll setup the development environment for the rest of the course. 

After setting up the environment, we will introduce a **CSS** framework for better web page creationg: **Bootstrap**.

## Topic 1.1   Creating and running a web page

<p align="center"><b>
Step 1 : Create and run an index.html file
</b></p>
                                   
                              
Let's create our first web page, starting from scratch and building block-by-block!

**What is a web page made of?**

Everything starts with a single **HTML** file that can be defined with the extension **.html**. 
It's a standard for most web servers to look for a file called **index.html**. Let's create a new folder in our workspace.

In this course, all webpages must be placed inside the folder **~/webpage_ws**. 
We are going to create a new page for each **unit example** and **unit exercise**.

For this unit, let's create a new folder called **unit_01**. In this folder, create the file **index.html**. 

* The file will be at **~/webpage_ws/unit_01/index.html** (It's very important to keep this structure!).

```html
<html>

<head>
    <title>My first web page for ROS!</title>
</head>

<body>
    <div>
        <h1>Hello from Robot Ignite Academy!</h1>
        <p>Let's connect our website to a ROS robot!</p>
    </div>
</body>

</html>
```
The folder structure must be like below:

![image](https://user-images.githubusercontent.com/20908007/228859577-fce04238-e962-4924-8ae8-698d47e0aba1.png)

Now, we want to visualize it as a regular web page, through the browser!
But first, we need to have a **web server** making this page available on the internet. 

# 

<p align="center"><b>
Step 2 : Run a web server 
</b></p>
         
Let's go to an available web shell and get into the folder that contains our web page 

```
$ cd ~/webpage_ws/unit_01
```

And start a HTTP web server:

```
$ python -m SimpleHTTPServer 7000
Serving HTTP on 0.0.0.0 port 7000 ...
192.168.0.1 - - [30/Mar/2023 14:12:35] "GET / HTTP/1.0" 200 -
```

Your web shell will get busy. Keep it like that, as the server must be running there.

It's chosen the port 7000 for our course because our platform makes the website available in a secure connection through this port.

In order to access the website, we offer you two options:

1. Use the **webpage** tab inside the course page: 

![Screenshot from 2023-03-30 16-13-00](https://user-images.githubusercontent.com/20908007/228864283-086e3cd7-3510-4191-a33c-8eb6cbb8d18e.png)


Every time you click over this button, the webpage is refreshed and you get the latest version of your code.

1. Open the webpage in a **new tab of your web browser or even on a different device!**


In order to do so, you need the **public address of our page.** 
In a similar way as we did to find out the address of the `rosbridge server`, we have to do this for the website server. 
In a different web shell, execute the command below:

```
$ webpage_address
```
You must get something similar to:
```
https://i-02131eed912e2497d.robotigniteacademy.com/6336074d-6041-4ed8-9368-754414639243/webpage/
```

## Topic 1.2   Adding some styles to the page

Let's make webpage a bit nicer.

A very famous library to construct layouts and beautify web pages is called **Bootstrap** (https://getbootstrap.com/). 

<p align="center"><b>
Step 3 :  Adding bootstrap library to the page  
</b></p>

There are two important things that make a web page look better. 
* You need to **create the structure (HTML)** and **add some styles (CSS)**. 
* 
We won't work with CSS in this course, since it's not about styling web pages, but will only use some existing styles to make our web page clearer.


