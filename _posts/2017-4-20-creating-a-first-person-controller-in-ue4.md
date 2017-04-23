---
layout: article
title:  "Creating a First Person Contoller in UE4"
date:   2017-4-22
categories: UE4 Tutorials
coverPhoto: http://ozgrozer.com/content/images/2016/06/startSSL.jpg
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

Now that our folders are created we want to save our level. To do that click **Save Current** in the toolbar at the top of the editor upon which you will be prompted with the following dialogue:

![alt text](http://i.imgur.com/3Q9lvRR.png "Saving the level")

Double click the **Levels** folder then give the level a name at the bottom, I named mine **Level01**. Then click **Save** to save our level in our Levels folder.

Next we want to set the editor to open our level everytime that we start it. To do this click on **Settings** in the toolbar at the top then click **Project Settings**.

![alt text](http://i.imgur.com/MtQ9feI.png "Opening Project Settings")

Once you do that you will be greeted with the **Project Settings** window. On the left sidefind and click on **Maps & Modes**. This will display your projects default maps and modes. Under the **Default Maps** section you will see two drop down boxes, one for **Editor Startup Map** and another for **Game Default Map**. We only need to worry about the **Editor Startup Map** for now. Click the drop down box and select the map that we saved.

![alt text](http://i.imgur.com/wGmKZBQ.png "Setting default map")

Now everytime we open the editor it will load our level. While we are in the project settings we will move on to setting up the player inputs.

<a name="inputs"></a>
### 2. Setting up Player Inputs
Once again on the left side of the **Project Settings** window, scroll down until you see **Inputs** and click on it. This will display the input manager where we can set which buttons will react to player input. Under bindings you will see **Action Mappings** and **Axis Mappings**. **Axis Mappings** are generally used for movement input while **Action Mappings** are used for actions like jumping or shooting.

![alt text](http://i.imgur.com/wjGepzE.png "Setting player inputs")

First we will ass the mappings for moving left, right, forward, and back. Start by click the **+** beside axis mappings then clicking the triangle that appears before **Axis Mappings**. Type **Right**  into the text box and then click the triangle before it. Click the drop down and type **D** into the search box then select the **D** key for the keyboard and make sure that **Scale** is set **1.0** 

![alt text](http://i.imgur.com/BZXwlZK.png "Setting D key")

No click the **+** next to the text box we typed **Right** into and another drop down will appear. Set that drop down to the **A** key on the keyboad the same way we selected the **D** key. For this one set the scale to **-1.0** because we want to move left when we press **A**

![alt text](http://i.imgur.com/fPhV7It.png "Setting A key")

Now we are going to do the same thing with **W** and **S** and are going to name it **Foward** as seen in the image below.

![alt text](http://i.imgur.com/drfYlzD.png "Foward input set up")

That is it for our **Axis Mappings** now we need to add a bind for jumping. That follows the same procedure but is created as an **Action Mapping** instead. Create a new **Action Mapping**, call it **Jump** and set it to **Space Bar** and make sure all the boxes beside it are **unchecked**. Our Final setup will look like the image below.

![alt text](http://i.imgur.com/VXztON9.png "Final input mapping")

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

Next click **Compile** and then **Save** at the top and close the blueprint editor.


<a name="gamemode"></a>
### 4. Creating a Custom Game Mode

Now we are going to create a custom game mode so that we can have our **FPSController** spawn as the default pawn when we play our game. To do this we will follow the same procedure as creating the **FPSController** blueprint but instead of selecting **Character** from the Pick Parent Class window we will click **Game Mode Base**. This will create a new game mode and it will appear in the Content Browser. Name our new game mode **BP_FPSGameMode**.

![alt text](http://i.imgur.com/4YzukHN.png "FPSGameMode in Content Browser")

Now we need to set our new game mode as our games default game mode. To do this we need to go back to the **Project Settings** do this by clicking **Settings > Project Settings**. On the left click **Maps & Modes**,  this will show the default maps and modes. Inder **Default Modes** click the drop down by **Default GameMode** and select the game mode we created.

![alt text](http://i.imgur.com/viiXDw4.png "Selecting default game mode")

Now click the triangle next to **Selected GameMode** and pick your **BP_FPSController** blueprint from the drop down next to **Default Pawn Class**. This tells the game mode to use our player controller as the default when playing the game.

![alt text](http://i.imgur.com/sNfq2he.png "Selecting default pawn")
 
 Thats it! Now our custom player controller will spawn when we play the game. To test if it is working close the **Project Settings** window and click **Play** on the toolbar at the top. You should not be able to move or look around. If you still can, press **Escape** then **ctrl+shift+s** to save all and then try it again.

<a name="movement"></a>
### 5. Creating the Player Movement

