---
layout: article
title:  "Improving Our First Person Controller"
date:   2017-4-23
categories: UE4 Tutorials
coverPhoto: http://i.imgur.com/BY6xyCO.png
---

Today we are going to make some improvements to the first person controller we made in the last tutorial. This tutorial will cover adding mouse look sensitivity and air control to our controller.

We will start by adding mouse look sensitivity. Open your **BP_FPSController** blueprint, to add sensitivity we have to adjust the value being sent to the **Val** pin on the **Add Controller Yaw Input** and **Add Controller Pitch Input** nodes. We will do this by multiplying a value with the value coming from the **Axis Value** pin on the **InputAxis MouseX** and **InputAxis MouseY** nodes. We will be adding seperate yaw and pitch input so the player has better control over their sensitivity. Start by adding two **float * float** nodes and connecting them according to the picture below.

![alt text](http://i.imgur.com/ErobkUF.png "Adding sensitivity")

Now we want to create two new float variables to make it easy to change the sensitivity at runtime later on. To do this click the **+** next to **Variables** on the left of the blueprint editor. Name this new variable **XSens** and make sure it is a **float**. To check if your new variable is a float look on the details window in the top left and make sure the settings match the image below.

![alt text](http://i.imgur.com/05zbAnA.png "creating float variable")

Create a **YSens** float variable following the same procedure. Once you have done that **compile** your blueprint so that we can set the default value of our new variables. Once you compile your blueprint a new value appears in the details panel on the left. We want to change this to **0.5** for both our **XSens** and **YSens** variables.

![alt text](http://i.imgur.com/vpJvQEq.png "default value for float variable")

Now we need to connect out new variables to the empty pins on the **float * float** nodes. Do this by holding **ctrl** and dragging the new sensitivity varaibles from the left onto the event graph and connect them to their respective **float * float** nodes. Holding **ctrl** while dragging and dropping the variable creates a node that gets the value of the variable which in our case is **0.5**.

![alt text](http://i.imgur.com/007OkzN.png "final sensitivity setup")

That's it! You can now set the sensitvity of your mouse look by changing the values of **XSens** and **YSens**.
