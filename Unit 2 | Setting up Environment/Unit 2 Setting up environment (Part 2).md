
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

 <!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 2.1 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 2.1   What is JavaScript ?  <a name="paragraph1"></a>

* JavaScript is a language created to help develop dynamic web pages.
* Dynamic web pages are the ones that **interact with user actions, updating the content, showing animations, or reacting to user data**. 

For reference about web and JavaScript foundations : https://developer.mozilla.org/en-US/docs/Learn/JavaScript

Web page contains HTML and can have CSS to add some style.  Now, to make things more interesting, we are going to add JavaScript to it.

* This programming language can **interact with external services, like APIs** through **assynchronous requests or websocket servers**.


<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 2.2 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

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

In order to access the **DevTools**, press F12 while you have a tab open. You must have a window like this one open:


![image](https://user-images.githubusercontent.com/20908007/229127061-07e6bbc2-78b0-48c2-befc-436dae9e88b3.png)

**2. Console** is where you can check the messages we output using the instruction console.log, and we'll use it to **identify errors** or just to better understand how our **code behaves**. 
  * It even shows the line of the code that produced the log. 

![image](https://user-images.githubusercontent.com/20908007/229128766-e876e8e6-023a-462a-95a9-1415283dc14b.png)


**3. Network** tab shows all the established connections between JavaScript and other sources.
  *  We will show it further when we have the **rosbridge connection established**.


<p align="center"><b>
Step 2 : - Debugging the tab inside the course page -
</b></p>

If you have opened the DevTools using the course page, instead of a new browser tab, you may have noticed a lot of messages and content that do not belong to the page you have created so far. 

In order to debug **only the webpage frame**, you have to choose it from the menu. Check the gif below:

![topic_02_demo_console](https://user-images.githubusercontent.com/20908007/229128217-567c0a02-8bcd-4c0e-9e9b-3cfa4d38c468.gif)



<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 2.3 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 2.3 Basic setup of Vue.js framework  <a name="paragraph3"></a>

**Vue.js** is a "Progressive JavaScript Framework", created to be adopted incrementally. 
* It means it can be **used in any web page** you may have, including the ones created from the bottom using a different framework. 


**Que : Why use a framework?**
* With JavaScript,  challenges we used to face in order to keep the appearance of the web site synchronized with the JavaScript logic. 

# 
<p align="center"><b>
Step 3 : Adding Vue.js library 
</b></p>

This time, we are not including a style file, but JavaScript, so it goes a bit different. 
Append the following instruction to the **head** tag:

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.min.js"></script>
```
Instead of a **link** tag, we use a script tag, also the attribute to reference the library is not **href**, but **src**.

# 
<p align="center"><b>
Step 4 :  Using Vue.js library 
</b></p>

Since we are going to program a lot in JavaScript, we want to keep things organized. 
The **first step** is to separate our JavaScript code from our **index.html** file


Let's create a new file, in the same folder as **index.html**. It's called **main.js**.
* And just after **footer** tag, let's add a reference to a file we have just created.

Remove the **script** tag that we created to show a message in the console.

At this point, our **head** must be like this:
```html
<head>
	<title>My first web page for ROS!</title>
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
	 crossorigin="anonymous">

	<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.min.js">
	</script>
</head>
```

And the end of **index.html** file like:

```html
	...
    </footer>
	<script src="main.js"></script>
</body>

</html>
```

# 
<p align="center"><b>
Step 5 : Trying Vue.js features
</b></p>

Now, try to use some features of **Vue.js**. Let's put some code into the **main.js** file.

```js
let vueApp = new Vue({
    el: "#vueApp",
    data: {
        menu_title: 'My menu title',
        main_title: 'Main title, from Vue!!',
    }
})
```

We are defining a new **Vue object**, identified by the **ID vueApp**. 
Everything inside the element with this ID can be accessed/modified by it.


Let's identify our **main** content with this ID.

In order to experiment with that, let's change the **index.html** file (only the main section):

```html
<!-- main content -->
<main id="vueApp">
    <div class="container">
        <div class="row">
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h3>{{ menu_title }}</h3>
                        <p>This is the left side of my web page. It occupies 33% of the total width</p>
                    </div>
                </div>
            </div>
            <div class="col-md-8">
                <div class="card">
                    <div class="card-body">
                        <h2 class="text-center">{{ main_title }}</h2>
                        <p>Here it goes the main content of my first web page, able to control ROS robots using web tools!</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</main>
```

**What did we do there?**

Basically, the values from our **Vue object**, from the **main.js** file, are going to fill the places **{{ menu_title }}** and **{{ main_title }}**. 

**OUTPUT :**

![Screenshot from 2023-03-31 15-49-56](https://user-images.githubusercontent.com/20908007/229138495-589db259-9228-471f-b7f4-4b5ce088bda3.png)



<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Topic 2.4 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Topic 2.4 Practice! <a name="paragraph4"></a>


Let's practice a bit more using VUE to change the content on the web page.


Change the two paragraphs we have **`(<p>)`** and make their content come from the javascript file, like we did for the subtitles.
**Files:**

<p align="center"><b>
index.html
</b></p>


```html
<!-- main content -->
<main id="vueApp">
    <div class="container">
        <div class="row">
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h3>{{ menu_title }}</h3>
                        <p>{{ p_content_01 }}</p>
                    </div>
                </div>
            </div>
            <div class="col-md-8">
                <div class="card">
                    <div class="card-body">
                        <h2 class="text-center">{{ main_title }}</h2>
                        <p>{{ p_content_02 }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</main>
```


<p align="center"><b>
main.js
</b></p>

```js
let vueApp = new Vue({
    el: "#vueApp",
    data: {
        menu_title: 'My menu title',
        main_title: 'Main title, from Vue!!',
        p_content_01: 'This is the left side of my web page. It occupies 33% of the total width',
        p_content_02: 'Here it goes the main content of my first web page, able to control ROS robots using web tools!',
    }
})
```

**OR**

<p align="center"><b>
main.js
</b></p>

```js
let vueApp = new Vue({
    el: "#vueApp",
    data: {
        menu_title: 'My menu title',
        main_title: 'Main title, from Vue!!',
        phrase: "This is the left side of my web page. It occupies 55% of the total width. This is the left side of my web page. Let's practice a bit more using VUE to change the content on the web page."
    }
})
```

**OUTPUT**
![Screenshot from 2023-03-31 16-15-13](https://user-images.githubusercontent.com/20908007/229145391-8a9f62ac-44b2-4f55-a5de-4121843fc973.png)




<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%  Questions %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

## Questions <a name="paragraph"></a>

1. What is Vue.JS

  * Vue.js is a frontend JavaScript framework, not a styling tool. 
  * While Vue.js does provide some styling capabilities, such as scoped CSS and inline styles, it is primarily used for building user interfaces and single-page applications using JavaScript.


2. How to start a Python Web Server on port 7000?
```
$ python -m SimpleHTTPServer 7000 
```

















