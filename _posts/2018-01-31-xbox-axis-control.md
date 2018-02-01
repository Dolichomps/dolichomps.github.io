---
title: Granular control with a gamepad
cover-image: CHANGEME
summary: Today we will learn to achieve granular control with a gamepad joystick in Godot by creating a very simple character controller to showcase it.
---

Howdy, we are going to make a simple character controller that allows the player to move to the left and right with the left joystick on their gamepad. The character's speed is going to be effected by how far we are pushing the joystick to the left or right, thus acheiving granular control of the character's speed. I have created a base project for us to work from, please download it [here](https://mega.nz/#!wdkh1A6T!iGDsntH7I8MWSiCdYgq2TpZj1lqX9c8SRzv-85Yma4k) and open it in the editor.

## Let's do this 👍 ##
Start by opening up the `Player.tscn` scene by double clicking on it in the file system panel. Now that's open let's create a new script on the `Player` node by selecting it in the scene panel and pressing the `Attach script` button. The `Attach Node Script` window will pop up, we will keep the settings as the defaults and click `Create`.

![Attach node script]({{ site.baseurl }}/img/AttachNodeScript.png)

This will create a new script named `Player.gd`, attach it to our Player node, and switch to the script editor. Remove all the content of your script except for `extends KinematicBody2d` and let's get coding.

## The programming part ⌨️ ##
We will start by creating a constant to hold our max speed as well as a variable to hold the value of our joystick axis.
{% highlight python %}
extends KinematicBody2D

const MAX_SPEED = 500
var axisValue
{% endhighlight %}