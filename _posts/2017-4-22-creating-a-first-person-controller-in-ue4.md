---
layout: post
title:  "Creating a First Person Contoller in UE4"
date:   2017-4-22
tags: [ue4 tutorials, first person, fps, blueprint]
feature: http://i.imgur.com/BY6xyCO.png
---

As the first in hopefully a series of tutorials I wanted to set up a base project for those who may want to follow along. To start with we are going to make a first person controller using blueprints as I feel that it will help familiarize new users with the blueprint editor while still creating something of use. This tutorial will contain the following:

 1. [Setting up a blank project](#blank)
 2. [Setting up player inputs](#inputs)
 3. [Creating the FPSController blueprint](#fps)
 4. [Creating a custom game mode](#gamemode)
 5. [Creating the player movement](#movement)

<a name="blank"></a>
### 1. Setting up a Blank Project

We will start by making a new project. You will want to chose to create a **blueprints project** with the **blank** template. Make sure you choose no starter content for now, as we can import that later if needed.

![alt text](http://i.imgur.com/OvtMwKz.png "Creating blank project")

Once the project has been created and the editor has loaded we are going to need to make 2 new folders named **Blueprints** and **Levels**. To do this simply **right click** in the content browser and choose **New Folder**.

![alt text](http://i.imgur.com/DaXTHLW.png "Creating folders")

Now that our folders are created we want to save our level. To do that click **Save Current** in the toolbar at the top of the editor upon which you will be prompted with the following dialog:

![alt text](http://i.imgur.com/3Q9lvRR.png "Saving the level")

Double click the **Levels** folder then give the level a name at the bottom, I named mine **Level01**. Then click **Save** to save our level in our Levels folder.

Next we want to set the editor to open our level every time that we start it. To do this click on **Settings** in the toolbar at the top then click **Project Settings**.

![alt text](http://i.imgur.com/MtQ9feI.png "Opening Project Settings")

Once you do that you will be greeted with the **Project Settings** window. On the left side find and click on **Maps & Modes**. This will display your projects default maps and modes. Under the **Default Maps** section you will see two drop down boxes, one for **Editor Startup Map** and another for **Game Default Map**. We only need to worry about the **Editor Startup Map** for now. Click the drop down box and select the map that we saved.

![alt text](http://i.imgur.com/wGmKZBQ.png "Setting default map")

Now every time we open the editor it will load our level. While we are in the project settings we will move on to setting up the player inputs.

<a name="inputs"></a>
### 2. Setting up Player Inputs

Once again on the left side of the **Project Settings** window, scroll down until you see **Inputs** and click on it. This will display the input manager where we can set which buttons will react to player input. Under bindings you will see **Action Mappings** and **Axis Mappings**. **Axis Mappings** are generally used for movement input while **Action Mappings** are used for actions like jumping or shooting.

![alt text](http://i.imgur.com/wjGepzE.png "Setting player inputs")

First we will ass the mappings for moving left, right, forward, and back. Start by click the **+** beside axis mappings then clicking the triangle that appears before **Axis Mappings**. Type **Right**  into the text box and then click the triangle before it. Click the drop down and type **D** into the search box then select the **D** key for the keyboard and make sure that **Scale** is set **1.0** 

![alt text](http://i.imgur.com/BZXwlZK.png "Setting D key")

No click the **+** next to the text box we typed **Right** into and another drop down will appear. Set that drop down to the **A** key on the keyboard the same way we selected the **D** key. For this one set the scale to **-1.0** because we want to move left when we press **A**

![alt text](http://i.imgur.com/fPhV7It.png "Setting A key")

Now we are going to do the same thing with **W** and **S** and are going to name it **Forward** as seen in the image below as well as for the **MouseX** and **MouseY** which can also be seen in the image below. For **MouseY** make sure you set the **Scale** to **1.0** or you will have inverted vertical controls.

![alt text](http://i.imgur.com/OPO8EfT.png "Final axis mappings")

That is it for our **Axis Mappings** now we need to add a bind for jumping. That follows the same procedure but is created as an **Action Mapping** instead. Create a new **Action Mapping**, call it **Jump** and set it to **Space Bar** and make sure all the boxes beside it are **unchecked**. Our Final setup will look like the image below.

![alt text](http://i.imgur.com/OlwPDOO.png "Final input mapping")

We are now done setting up all the inputs we need to basic player controls. Feel free to close the **Project Settings** window, no need to save it does that automatically.

<a name="fps"></a>
### 3. Creating the FPSController Blueprint

Now it is time to create our **FPSController** blueprint. To do this double click on your **Blueprints** folder then right click anywhere in the Content Browser. This will open a menu and from the menu select **Blueprint Class**.

![alt text](http://i.imgur.com/meHPUc1.png "Create Blueprint Class")

This will open the **Pick Parent Class** window. We are making a character so we will click on **Character**. This will create a new **Character Blueprint** which will appear in the Content Browser. Name this new blueprint **BP_FPSController** as shown below.

![alt text](http://i.imgur.com/CpABjIN.png "FPSController in Content Browser")

Now we need to add a camera to the player controller so that we can see when we start the game. To do this double click on your **BP_FPSController** to open the blueprint editor. If you see the image below click **Open Full Blueprint Editor** at the top.

![alt text](http://i.imgur.com/WR4NDjS.png "open full blueprint editor")

You should see the blueprint editor, click the **Viewport** tab at the top to switch to the following window.

![alt text](http://i.imgur.com/2gqI3T2.png "viewport window")

This is where we will add our camera. To do this click the green **+ Add Component** button in the **Components** window in the top left and search for **Camera**.

![alt text](http://i.imgur.com/spn0mG1.png "adding camera component")

Name this component **Camera**, you will see it appear in the viewport. lick and drag the **blue arrow** up to change the cameras **Z location** to something more eye level.

![alt text](http://i.imgur.com/38d29T6.png "moving camera component")

Before we close the blueprint editor we need make sure the pawn users the controller rotation pitch so that we can look up and down. To do this make sure that the **BP_FPSController** is selected in the components window and on the right side under **Pawn** check the box beside **Use Controller Rotation Pitch**.

![alt text](http://i.imgur.com/jqsUwB5.png "Use Controller Rotation Pitch")

Once you have don that click **Compile** and then **Save** at the top and close the blueprint editor.


<a name="gamemode"></a>
### 4. Creating a Custom Game Mode

Now we are going to create a custom game mode so that we can have our **FPSController** spawn as the default pawn when we play our game. To do this we will follow the same procedure as creating the **FPSController** blueprint but instead of selecting **Character** from the Pick Parent Class window we will click **Game Mode Base**. This will create a new game mode and it will appear in the Content Browser. Name our new game mode **BP_FPSGameMode**.

![alt text](http://i.imgur.com/4YzukHN.png "FPSGameMode in Content Browser")

Now we need to set our new game mode as our games default game mode. To do this we need to go back to the **Project Settings** do this by clicking **Settings > Project Settings**. On the left click **Maps & Modes**,  this will show the default maps and modes. Under **Default Modes** click the drop down by **Default GameMode** and select the game mode we created.

![alt text](http://i.imgur.com/viiXDw4.png "Selecting default game mode")

Now click the triangle next to **Selected GameMode** and pick your **BP_FPSController** blueprint from the drop down next to **Default Pawn Class**. This tells the game mode to use our player controller as the default when playing the game.

![alt text](http://i.imgur.com/sNfq2he.png "Selecting default pawn")
 
 That's it! Now our custom player controller will spawn when we play the game. To test if it is working close the **Project Settings** window and click **Play** on the toolbar at the top. You should not be able to move or look around. If you still can, press **Escape** then **ctrl+shift+s** to save all and then try it again.

<a name="movement"></a>
### 5. Creating the Player Movement

Now it is time to create the logic to make our player move. We will start by opening the **BP_FPSController** blueprint. Upon opening you will be greeted with the **Event Graph**, if not click the **Event Graph** tab at the top.

![alt text](http://i.imgur.com/v6KPrQX.png "BP_FPSController event graph")

Click and drag to select the three nodes that are added by default, we won't need those. We will start by adding the ability to look around with the mouse to our player. **Right click** and type **Input** in the search box to display the list of input bindings. Select **MouseX** from **Action Events** and place it in the even graph. Do the same for **MouseY**.

![alt text](http://i.imgur.com/Xa08gLe.png "Adding mouseX and mouseY nodes")

We now want to connect the **InputAxis MouseX** to an **Add Controller Yaw Input** node and the **InputAxis MouseY** to an **Add Controller Pitch Input**. Then select all the nodes and press **C** to create a comment for those nodes. The setup will look like the image below.

![alt text](http://i.imgur.com/9GCcSha.png "Mouse look setup")

That's it for mouse look, press **Compile** and **Save** then close the blueprint editor and press play to test your game, you should now have mouse look.

Time to add player movement. Open the **BP_FPSController** blueprint back up and add your **InputAxis Forward** and **InputAxis Right** nodes the same way we added the mouse look nodes.

![alt text](http://i.imgur.com/yDlKaQm.png "Movement nodes")

Next we want to connect each of our new nodes to an **Add Movement Input** node as shown below.

![alt text](http://i.imgur.com/kgG4uMl.png "Add movement input")

We now need to set what direction the player will move in when we press the movement keys. But we only want movement on the **X and Y plane** and we want the player to be able to move around while looking at the ground. To do this we need to add a **Get Control Rotation** and right click on **Return Value** and select **Split Struct Pin**  so we can access the individual rotations.

![alt text](http://i.imgur.com/uWre13X.png "Split struct")

Now add a **Make Rotator** node and connect the **Return Value Z (Yaw)** pin from the **Get Control Rotation** node to the **Z (Yaw)** pin on the **Make Rotator** node.

![alt text](http://i.imgur.com/Bi1VWF0.png "Connect to Make Rotator")

Next add a **Get Forward Vector** node as well as a **Get Right Vector** node and connect the **Return Value** pin from the **Make Rotator**  to the **In Rot** node on both the **Get Forward Vector** and **Get Right Vector** nodes. Finally connect the **Return Value** pin from the **Get Forward Vector** to the **World Direction** pin on the **Add Movement Input** node for the **InputAxis Forward** and connect the **Get Right Vector** to the **Add Movement Input** for the **InputAxis Right** node. The final ...(line truncated)...

![alt text](http://i.imgur.com/DvJZbIx.png "Final Movement Input")

You will now have the ability to move your player around in the world. Now all we have to do is add jumping.

Jumping is surprisingly the easiest part. We start by adding the **Jump** action event node. Then we will connect the **Pressed** pin to a node called **Jump** and that's it jumping is done. The final setup is shown below.

![alt text](http://i.imgur.com/D20Sreb.png "Final Jump Input")

That's everything! Congratulations on creating your very own first person controller blueprint. Press play and try it out!