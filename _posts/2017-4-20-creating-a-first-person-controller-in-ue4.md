---
layout: article
title:  "Creating a First Person Contoller in UE4"
date:   2017-4-22
categories: UE4 Tutorials
coverPhoto: http://ozgrozer.com/content/images/2016/06/startSSL.jpg
---

As the first in hopefully a series of tutorials I wanted to set up a base project for those who may want to follow along. To start with we are going to make a fisrt person controller using blueprints as I feel that it will help familiarize new users with the blueprint editor while still creating something of use. This tutorial will contain the following:

 1. [Setting up a blank project](#blank)
 2. [Setting up player inputs](#inputs)
 3. [Creating a FPSController blueprint](#fps)
 4. [Creating a custom game mode](#gamemode)
 5. [Creating the player movement](#movement)

___

###<a name="blank"></a>1. Setting up a Blank Project
We will start by making a new project. You will want to chose to create a **blueprints project** with the **blank** template. Make sure you choose no starter content for now, as we can import that later if needed.

![alt text](http://i.imgur.com/OvtMwKz.png "Creating blank project")

Once the project has been created and the editor has loaded we are going to need to make 2 new folders named **Blueprints** and **Levels**. To do this simply **right click** in the content browser and choose **New Folder**.

![alt text](http://i.imgur.com/DaXTHLW.png "Creating folders")

Now that our folders are created we want to save our level. To do that click **Save Current** in the toolbar at the top of the editor upon which you will be prompted with the following dialogue:

![alt text](http://i.imgur.com/3Q9lvRR.png "Saving the level")

Double click the **Levels** folder then give the level a name at the bottom, I named mine **Level01**. Then click **Save** to save our level in our Levels folder.
