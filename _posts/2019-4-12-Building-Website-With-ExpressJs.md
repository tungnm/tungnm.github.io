---
layout: post
title: Building simple website with Express
---

# Overview
This tutorial walk you through the process of building a website using Node.Js and Express. Node is a generic server framework that can do many things. Express is a library of Node for serving websites. Better understanding of Express will come with more coding.

# Part I - Website: Hello world
After this exercise you can go to a browser and type in the url: http://localhost:3000/hello to get a message replied from the server.
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

The first line: *var express = require('express');** simply includes the Express library and assign the library to the variable named **express**

Second line: *var app = express();* creates a new object of the Express Web Server class and assign the object to the variable named **app**. These first 2 lines will always appear in all of your Express applications, so no need to spent too much time understanding them.

Next: *app.get('/hello', processRequest);* . This tells the web server: when someone requests a url with the path */hello* call the function named **processRequest**. The function is defined below. Now this is a fundamental step that you have to understand.
