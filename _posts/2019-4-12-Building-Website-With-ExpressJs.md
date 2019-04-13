---
layout: post
title: Building simple website with Express
---

# Overview
This tutorial walk you through the process of building a website using Node.Js and Express. Node is a generic server framework that can do many things. Express is a library of Node for serving websites. Better understanding of Express will come with more coding.

# Part I - Website: Hello world
The goal of this part is to setup a web server running locally in your laptop. The server listens for connection from local browser with the path: http:localhost:3000/hello and return a text "Hello world".
## Step 1 Installation
* [Install Node.js](https://nodejs.org/en/download/)
* Open terminal and create a folder for the project: `mkdir ~/nodeProject && cd ~/nodeProject`
* Install Express: `npm install --save express`

## Step 2 Initialize the project
* run `npm init`. This command asks few questions and setup the Node project for you. Simply press Enter on any field to use the default value.

## Step 3 Write the server code
Any text editing software is Ok but highly recommend[Visual Studio Code](https://code.visualstudio.com/Download)

Create a new file call server.js and enter the following code:
```javascript
var express = require('express');
var app = express();

app.get('/hello', processRequest);
app.listen(3000);

function processRequest(request, response) {
    console.log('Client request received');
    response.send('Hello world');
}
```
After saving the file, go to terminal and type: `node server.js` . This command starts your Node application. Now go to any browser and type in the url: `localhost:3000/hello`. You will see 2 things:
* `Hello world` shows up in your browser
* In the terminal, you see: `Client request received.`

### Javascript quick bite
Let's take a look at server.js file. The language of Node.js is Javascript. There are few things to notice when looking into this file.

First is the variable declaration: *var express = require('express')*. Note the key word **var** which is strange if you come from another programming language. Javascript does not require a variable to have type so every declaration would start with **var**. In C++ for example, to declare an integer and a String, you need to do:
```java
int x = 1;
String name = "Tung";
```
In Javascript, things get simpler, you just do:
```javascript
var x = 1;
var name = "Tung";
```
The reason is because javascript language try to intepret a type of a variable at runtime, and do a best guess for the type. This type-less characteristic is also true for function. If you look at the function definition below: *function processRequest(request, response)*. There is no return type either, because of the same reason.

### What happen behind the scene
Ok, with the quick note on Javascript, let's take a look at `server.js` again.

The first line: *var express = require('express');* simply includes the Express library and assign the library to the variable named **express**

Second line: *var app = express();* creates a new object of the Express Web Server class and assign the object to the variable named **app**. These first 2 lines will always appear in all of your Express applications, so no need to spent too much time understanding them.

Next: *app.get('/hello', processRequest);* . This tells the web server: when someone requests a url with the path */hello* call the function named **processRequest**. The function is defined below. This is a fundamental step that you have to understand. 

This functions is not any function, it has to take in 2 parameters: *function processRequest(request, response)*. **request** includes any information that a user wants to send to the server. Your server code typically reads information from **request** for processing. Example of **request** information is new user registration with email, name, address ; a book name user want to search for... 

**response** is the object that your server put data into, to send back to the browser. In this example, the server use *response.send('Hello world');* to send the reply back.

Last line: *app.listen(3000);* . This gets the server to start listening on port 3000 for any connection from clients. Whenever a client connects(someone user the browser to hit the url), the function **processRequest** is called. Note that your port number on the url needs to match with this number, so *http://localhost:2999/hello* would not work.

###Excercise
Change the server code so that *http://localhost:2999/about* also returns a short message describing the website
