### Table of contents
1. [Topic 1.1   Creating and running a web page](#paragraph1)
2. [Topic 1.2   Adding some styles to the page](#paragraph2)
3. [Topic 1.3   Let's Practice!](#paragraph3)

# Unit 1:   Setting up our development environment (Part 1)

**- Summary -**
 
This unit is a general idea about web development.
We'll setup the development environment for the rest of the course. 

After setting up the environment, we will introduce a **CSS** framework for better web page creationg: **Bootstrap**.
 
## Topic 1.1   Creating and running a web page  <a name="paragraph1"></a>

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

## Topic 1.2   Adding some styles to the page <a name="paragraph2"></a>

Let's make webpage a bit nicer.

A very famous library to construct layouts and beautify web pages is called **Bootstrap** (https://getbootstrap.com/). 

<p align="center"><b>
Step 3 :  Adding bootstrap library to the page  
</b></p>

There are two important things that make a web page look better. 
* You need to **create the structure (HTML)** and **add some styles (CSS)**. 

We won't work with CSS in this course, since it's not about styling web pages, but will only use some existing styles to make our web page clearer.

The first step to add some style is to add the library we are going to use.

In order to do this, add to the `<head>` section of your **index.html** the following:
 
 ```html
<head>
    <title>My first web page for ROS!</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
```
# 

<p align="center"><b>
Step 4 :  Adjusting HTML to use styles 
</b></p>

 There are some different ways a **CSS** file can change the **HTML** appearance. 
 It can customize the elements by the **tag, class, id,** and other selectors that, for the sake of simplicity, we won't use.

If you just reload the web page, you will notice that it is slightly different because of the **tag selectors** of the bootstrap library.

Now, we are going to use some **classes**.
Let's modify the **HTML** in order to use them. 

```html
<html>

<head>
	<title>My first web page for ROS!</title>
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
	 crossorigin="anonymous">
</head>

<body class="d-flex flex-column h-100">
	<!-- header of the page -->
	<header class="header">
		<div class="container">
			<div class="jumbotron text-center">
				<h1>Hello from Robot Ignite Academy!</h1>
				<p>Let's connect our website to a ROS robot!</p>
			</div>
		</div>
	</header>

	<!-- main content -->
	<main>
		<div class="container">
			<div class="row">
				<div class="col-md-4">
					<div class="card">
						<div class="card-body">
							<h3>Menu</h3>
							<p>This is the left side of my web page. It occupies 33% of the total width</p>
						</div>
					</div>
				</div>
				<div class="col-md-8">
					<div class="card">
						<div class="card-body">
							<h2 class="text-center">Main content</h2>
							<p>Here it goes the main content of my web page.</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</main>

	<!-- footer -->
	<footer class="footer mt-auto bg-dark text-light">
		<div class="container">
			<h5>page ends here!</h5>
		</div>
	</footer>
</body>

</html>
```

You must have a pretty web page with styles and harmony between the elements! 

 ![image](https://user-images.githubusercontent.com/20908007/228871698-f61f2ac3-e7f3-4fac-808c-e9dee65bc3bf.png)

 
* If you go through the **HTML** code, you will notice that we have added many different **tags** and **classes**. 
 
For example: Some **div** elements belong to the class **container**, which describes the behavior of having a **block that fits the entire width of the page**.

**Note :** The **grid system** that allows us to define **rows** (we have a div using the class **row**).
It defines an element that fills the entire width of a **container**. Inside a row, we have **columns**. 
Now, here's the trick! Every row must have **12** (yes, exaclty 12!!) units of columns


In our case, we created just **2 columns**,
 * but we defined the **first one with [4]** units (**col-md-4**) and the second with [**8**] units (**col-md-8**).

The **-md-** means it will be applied to **medium size pages**. You can check the size definition below (taken from bootstrap page):

* Extra small (**xs**) : width is **< 576px**
* Small (**sm**) : width is **≥576px**
* Medium (**md**) : width is **≥768px**
* Large (**lg**) : width is **≥992px**
* Extra large (**xl**) : **≥1200px**


If you want to better understand the **grid system**,

* please check this page: https://getbootstrap.com/docs/4.3/layout/grid/

![Screenshot from 2023-03-30 16-44-57](https://user-images.githubusercontent.com/20908007/228873876-5365711c-396e-4fe3-88a8-eed9d98dc6cc.png)

We have also used a very modern and nice element, called **card**. 

* Please check the reference here: https://getbootstrap.com/docs/4.3/components/card/

![image](https://user-images.githubusercontent.com/20908007/228874876-ea071fca-33ee-4de5-b31b-cb90570c65ca.png)



## Topic 1.3   Let's Practice! <a name="paragraph3"></a>

<p align="center">
- Exercise 1.3 -
</p>

Let's fix the knowledge of html + css using the bootstrap library to define grids. 

* Instead of occupying sizes of **4 and 8**, change the columns to use half in each one, if the page is **large**. 
* Make it occupy the entire width of each one, if the webpage is small (**sm**).

*Remember you can test it by resizing the screen. Also try using not only the webpage render of the course page, but another tab, by copying the webpage_address value and opening it.*

<p align="center">
Ex index.html  : 
</p>

```html
<html>

<head>
    <title>My first web page for ROS!</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>

<body class="d-flex flex-column h-100">
    <!-- header of the page -->
    <header class="header">
        <div class="container">
            <div class="jumbotron text-center">
                <h1>Hello from Robot Ignite Academy!</h1>
                <p>Let's connect our website to a ROS robot!</p>
            </div>
        </div>
    </header>

    <!-- main content -->
    <main>
        <div class="container">
            <div class="row">
                <div class="col-md">
                    <div class="card">
                        <div class="card-body">
                            <h3>Menu</h3>
                            <p>This is the left side of my web page. It occupies 33% of the total width</p>
                        </div>
                    </div>
                </div>
                <div class="col-md">
                    <div class="card">
                        <div class="card-body">
                            <h2 class="text-center">Main content</h2>
                            <p>Here it goes the main content of my web page.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- footer -->
    <footer class="footer mt-auto bg-dark text-light">
        <div class="container">
            <h5>page ends here!</h5>
        </div>
    </footer>
</body>

</html>

<html>

<head>
    <title>My first web page for ROS!</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>

<body class="d-flex flex-column h-100">
    <!-- header of the page -->
    <header class="header">
        <div class="container">
            <div class="jumbotron text-center">
                <h1>Hello from Robot Ignite Academy!</h1>
                <p>Let's connect our website to a ROS robot!</p>
            </div>
        </div>
    </header>

    <!-- main content -->
    <main>
        <div class="container">
            <div class="row">
                <div class="col-md">
                    <div class="card">
                        <div class="card-body">
                            <h3>Menu</h3>
                            <p>This is the left side of my web page. It occupies 33% of the total width</p>
                        </div>
                    </div>
                </div>
                <div class="col-md">
                    <div class="card">
                        <div class="card-body">
                            <h2 class="text-center">Main content</h2>
                            <p>Here it goes the main content of my web page.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- footer -->
    <footer class="footer mt-auto bg-dark text-light">
        <div class="container">
            <h5>page ends here!</h5>
        </div>
    </footer>
</body>

</html>
``



