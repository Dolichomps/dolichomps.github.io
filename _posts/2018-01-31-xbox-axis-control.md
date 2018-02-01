---
title: Granular control with a gamepad
cover-image: CHANGEME
summary: Today we will learn to achieve granular control with a gamepad joystick in Godot by creating a very simple character controller to showcase it.
---

Howdy, we are going to make a simple character controller that allows the player to move in any direction with the left joystick on their gamepad. The character's speed is going to be effected by how far we are pushing the joystick in the respective direction, thus acheiving granular control of the character's speed. I have created a base project for us to work from, please download it [here](https://mega.nz/#!wdkh1A6T!iGDsntH7I8MWSiCdYgq2TpZj1lqX9c8SRzv-85Yma4k) and open it in the editor.

## Let's do this 👍 ##
Start by opening up the `Player.tscn` scene by double clicking on it in the file system panel. Now that's open let's create a new script on the `Player` node by selecting it in the scene panel and pressing the `Attach script` button. The `Attach Node Script` window will pop up, we will keep the settings as the defaults and click `Create`.

![Attach node script]({{ site.baseurl }}/img/AttachNodeScript.png)

This will create a new script named `Player.gd`, attach it to our Player node, and switch to the script editor. Remove all the content of your script except for `extends KinematicBody2d` and let's get coding.

## The programming part ⌨️ ##
We will start by creating a constant to hold our max speed, and variables to hold our controller deadzone, joystick axis value, and current motion.

{% highlight javascript %}
extends KinematicBody2D

const MAX_SPEED = 500

var deazone = 0.2
var axisValue = Vector2()
var motion = Vector2()
{% endhighlight %}

Since we are moving a character we want its movement logic to be framerate independent, this mean we will use the `_physics_process` function to update our character's postion. Each physics update we reset our movement vector to (0, 0) then set the `axisValue` vector to the value that the joystick is at on both x and y. Then if the axis value is greater than the deadzone we update the motion vector and then move the character. Let's see what that looks like.

{% highlight javascript %}
extends KinematicBody2D

const MAX_SPEED = 500

var deazone = 0.2
var axisValue = Vector2()
var motion = Vector2()

func _physics_process(delta):
    # reset the motion vector
    motion = Vector2()
    
    # store the joy axis x and y value
    # Input.get_joy_axis(int device, int axis) returns a value between -1 and 1
	axisValue.x = Input.get_joy_axis(0, 0)
	axisValue.y = Input.get_joy_axis(0, 1)
    
    # check if the axis value is more than the deadzone
    # must use absolute value because avisValue can be negative
	if (abs(axisValue.x) > deadzone or abs(axisValue.y) > deadzone):
		motion = (axisValue * MAX_SPEED) * delta
    
    # move on the motion vector and check for collision
	move_and_collide(motion)
{% endhighlight %}

Believe it or not that is all the code we need, press the play button in the top right or just press f5 and you should be greeted with a little character you can move around with your gamepad with speed that increases with how far you push the joystick.

![Game]({{ site.baseurl }}/img/game.gif)

That is it for this tutorial, if you would like to download the finished project you can get it [here](https://mega.nz/#!QA0xjAyK!eGrzhu05rF0draESkhI62LjUHipaEPBcgJ9_wqhlcCI).
