---
layout: post
title:  "Improving Our First Person Controller"
date:   2017-4-23
tags: [ue4 tutorials, first person, fps, blueprint]
feature: http://i.imgur.com/DCfQUAd.png
---

Today we are going to make some improvements to the first person controller we made in the last tutorial. This tutorial will cover adding mouse look sensitivity and air control to our controller.

### 1. Adding Mouse Look Sensitivity

We will start by adding mouse look sensitivity. Open your **BP_FPSController** blueprint, to add sensitivity we have to adjust the value being sent to the **Val** pin on the **Add Controller Yaw Input** and **Add Controller Pitch Input** nodes. We will do this by multiplying a value with the value coming from the **Axis Value** pin on the **InputAxis MouseX** and **InputAxis MouseY** nodes. We will be adding separate yaw and pitch input so the player has better control over their sensitivity. Start by adding two **float * float** nodes and connecting them according to the picture below.

<figure>
    <a href="http://i.imgur.com/ErobkUF.png"><img src="http://i.imgur.com/ErobkUF.png"></a>
</figure>

Now we want to create two new float variables to make it easy to change the sensitivity at runtime later on. To do this click the **+** next to **Variables** on the left of the blueprint editor. Name this new variable **XSens** and make sure it is a **float**. To check if your new variable is a float look on the details window in the top left and make sure the settings match the image below.

<figure>
    <a href="http://i.imgur.com/05zbAnA.png"><img src="http://i.imgur.com/05zbAnA.png"></a>
</figure>

Create a **YSens** float variable following the same procedure. Once you have done that **compile** your blueprint so that we can set the default value of our new variables. Once you compile your blueprint a new value appears in the details panel on the left. We want to change this to **0.5** for both our **XSens** and **YSens** variables.

<figure>
    <a href="http://i.imgur.com/vpJvQEq.png"><img src="http://i.imgur.com/vpJvQEq.png"></a>
</figure>

Now we need to connect out new variables to the empty pins on the **float * float** nodes. Do this by holding **ctrl** and dragging the new sensitivity variables from the left onto the event graph and connect them to their respective **float * float** nodes. Holding **ctrl** while dragging and dropping the variable creates a node that gets the value of the variable which in our case is **0.5**.

<figure>
    <a href="http://i.imgur.com/007OkzN.png"><img src="http://i.imgur.com/007OkzN.png"></a>
</figure>

That's it! You can now set the sensitivity of your mouse look by changing the values of **XSens** and **YSens**.

### 2. Adding Air Control

Thanks to Unreal Engine's awesome character class that our **BP_FPSController** is based of off adding air control is super easy. In our **BP_FPSController** blueprint select the **CharacterMovement** component from the **Components** panel in the top left. Once selected the **Details** panel on the right will be full of options. Here you can change all aspects of your characters movement, scroll down until you see **Character Movement: Jumping/Falling**. Under that heading there are a bunch of options, the one we are focused on is **Air Control**. I am going to set mine to **1.0** so that my character has full control while in the air. Feel free to set this value to whatever suites you.

<figure>
    <a href="http://i.imgur.com/kT0y4hK.png"><img src="http://i.imgur.com/kT0y4hK.png"></a>
</figure>

**Compile** and **Save** your blueprint and test out your improved first person controller!