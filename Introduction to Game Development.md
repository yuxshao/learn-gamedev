<a id="top"></a>
# Introduction to Game Development

*Design Principles and Game Maker*

Written and developed by [CU Game Dev](http://cugamedev.org/) and [ADI](adi).

<a href="#top" class="top" id="getting-started">Top</a>
## About This Document
### Methodology
This guide will guide you through making two simple games. One will be a top-down shooter style game that will help you become familiar with the GameMaker program that we will be using and with the concept of a MVP (minimum viable product). Afterwards, you will be guided on making a more complex platformer-style game, building upon what we have learned previously.

### Prerequisites
Installing the GameMaker program. No prior coding knowledge is required.

To install GameMaker, go to http://www.yoyogames.com/studio. Click the free download, and then install the program on your computer. 

### The End Product
2 games, one a simple top-down shooter, another being a more complex platformer.

You can find sample code on [GitHub][github]

<a href="#top" class="top" id="table-of-contents">Top</a>
## Table of Contents

-	[Level 1: General Intro to Game Design and Programming](#level1)
	-	[1.1 Game Design considerations](#game-design-considerations)
		-	[1.1.1 What makes a good game?](#What-makes-a-good-game)
		-	[1.1.2 Things to focus on](#Things-to-focus-on)
		-	[1.1.3 How we develop games](#how-we-develop-games)
	-	[1.2 Game Programming](#game-programming)
		-	[1.2.1 Game Loop] (#game-loop)
		-	[1.2.2 Update Method] (#update-method)
		-	[1.2.3 Other common themes] (#other-themes)
	-	[1.3 Minimum Viable Product] (#MVP)
		-	[1.3.1 What is it?](#bare-bones)
		-	[1.3.2 Uses of the MVP](#uses-MVP)
	-	[1.4 Tools Used in the Game Industry](#tools-used)
		-	[1.4.1 List of various game engines] (#list-engines)
		-	[1.4.2 List of other tools] (#list-tools)
		
-	[Level 2: Your First Game! Making an MVP](#top-down-shooter)
	-	[2.1 Parts of GameMaker](#GM-parts)
	-	[2.2 A Basic Top-Down Shooter](#basic-top-down-shooter)
		-	[2.2.1 Creating Resources - Sounds and Sprites](#create-resource-sounds-sprites)
		-	[2.2.2 Basic Game Logic](#basic-game-logic)
		-	[2.2.3 Object Interaction - Enemies](#object-interation-enemies)
		-	[2.2.4 Control Flow & Variables - Health](#control-flow-variables-health)
		-	[2.2.5 Alarms and Periodic Events](#alarms-periodic)
		-	[2.2.6 Let's Polish our Game!](#polish)
	-	[2.3 Let's Review Level 2!](#basic-top-down-shooter)
-	[Level 3: Creating a Platformer](#level3)
	-	[3.1 Resource Setup](#resource-setup)
	-	[3.2 Scripts & the Step Event](#scripts-step-events)
		-	[3.2.1 The Step Event](#step-event)
		-	[3.2.2 Game Maker Language](#GM-language)
		-	[3.2.3 Game Maker Defaults](#GM-defaults)
	-	[3.3 Horizontal Movement](#horizontal-movement)
		-	[3.3.1 A First Attempt](#first-attempt)
		-	[3.3.2 Smooth Movement](#smooth-movement)
	-	[3.4 Vertical Movement](#vertical-movement)
		-	[3.4.1 Gravity](#gravity)
		-	[3.4.2 Jumping](#jumping)
		-	[3.4.3 Stopping Your Jump](#stopping-your-jump)
		-	[3.4.4 Walking Animation](#walking-animation)
	-	[3.5 Platform Collision](#platform-collision)
		-	[3.5.1 Landing on a Block](#landing-block)
		-	[3.5.2 Hitting a Block from the Bottom](#hitting-block-bottom)
		-	[3.5.3 Hitting the Side of the Block](#hitting-block-side)
		-	[3.5.4 Horizontal or Vertical Collision?](#horizontal-verticle)
		-	[3.5.5 Jumping at the Right Time](#jump-right-time)
		-	[3.5.6 Optional: A Quirk with GameMaker](#optional-quirk)
	-	[3.6 Views](#views)
	-	[3.7 Tiles](#tiles)
	-	[3.8 A Few Additions](#additions)
		-	[3.8.1 Enemies](#enemies)
		-	[3.8.2 Coins](#coins)

-	[Level 4: States and Menus](#level4)
	-	[4.1 States](#states)	
-	[Level 5: Design Considerations](#level5)
-   [Additional Resources](#additionalresources)


------------------------------
<a href="#top" class="top" id="level1">Top</a>
## Level 1: General Intro to Game Design and Programming


<a href="#top" class="top" id="game-design-considerations">Top</a>
## 1.1 Game Design Considerations

<a id="What-makes-a-good-game"></a>

### 1.1.1 What makes a good game?

If you're interested in making a game, you must have played a few games here and there. As you know, there isn't a definitive definition of what a "good" game is. A game that you think is amazing might be so-so to your friend, and vice versa. However, there are certain points of games that make them stand out from the crowd. Generally, good games give the player enough freedom to do as they please, but still give a set of rules that the player must follow. The set of rules is what we can call the mechanic of the game, which will be expanded upon later.

<a id="Things-to-focus-on"></a>
### 1.1.2 Things to Focus on

When building your game, there are a few points to consider before tackling your project. First and foremost, the game you make, either on your own or with a group, should be something that is managable, in both complexity and size. Another point to think about is the engine that you will be using when developing your game. Various engines come with different capabilities, which will influence what your game will be like. 

When planning out your project, it is important to give yourself guidelines of when you want certain parts of the game to be in a completed state. By giving yourself a calendar to work with will allow you and your group to be more organized when creating your project.

Finally, when planning out your game, make sure it is something that you would enjoy playing, as well as developing!

<a id="how-we-develop-games"></a>
### 1.1.3 How we Develop Games

There are many ways to develop games, however, in this lesson we will be focused on developing a game centered around a mechanic.

<a href="#top" class="top" id="game-programming">Top</a>
## 1.2 Game Programming

Programming patterns and concepts from other types of software are also common in games, but a game in particular is a sort of simulation of a set of rules for the game universe. Because of this, the code structure for a game typically follows two patterns:

<a id="game-loop"></a>
###1.2.1 The Game Loop
In a game, the core of the logic is contained in a loop running indefinitely, with each run of the loop simulating a number of “steps” of the game universe, followed by a render of the universe, and then a delay keeps the simulation running at a reasonable speed (e.g., 60fps).

<a id="update-method"></a>
###2.2.2 The Update Method
Most games involve entities, like players, enemies, or powerups, interacting with each other. To capture this, game engines typically divide game logic into packages called objects, each of which, in each step of the game universe, has its own behavior.
Depending on the game you want to make, the variety of programming, math, and physics concepts you might need are endless, from pathfinding to gravity to finite state machines. The two key concepts that games use, though, are the game loop and update method. Try to keep these two ideas in the back of your mind as we see how Game Maker games are structured following this system.


<a href="#top" class="top" id="MVP">Top</a>
## 1.3 Minimum Viable Product

<a id="bare-bones"></a>
### 1.3.1 What is a Minimum Viable Product?

A Minimum Viable Product (henceforth 'MVP') is a bare bones version of your game. This is a stage where there will be no art or music in your game and usually the game will consist of one level or room of your game.


<a id="uses-MVP"></a>
### 1.3.2 Uses of the MVP

This is used mainly in testing purposes to see if your mechanic works as intended. By having an MVP, you can work out any bugs, allow others to test your game's mechanic, and start tweaking things to your liking.


<a href="#top" class="top" id="tools-used">Top</a>
## 1.4 Tools used in the Gaming Industry

The Game Development industry uses a plethora of tools when developing games. From the small indie studios to the large triple-A productions, these tool are used in the creation of all sorts of games.

<a id="list-engines"></a>
### 1.4.1 List of game engines

Here's a list of some of the game engines that are used:

Unity
Unreal Engine
GameMaker
RPG Maker
Twine

<a id="list-tools"></a>
### 1.4.2 List of various other tools

These might come in handy later on when creating assets, music, and other parts of your game.

Autodesk Maya 
Adobe Illustrator, Photoshop, etc.
Audacity (free music editor)


___________
<a href="#top" class="top" id="top-down-shooter">Top</a>
## Level 2: Your First Game! Making an MVP

<a href="#top" class="top" id="GM-parts">Top</a>
### 2.1 Parts of GameMaker

In GameMaker, a game is made up of various parts. Here we'll describe each part and their function before we move on to using them when making our basic game.

Sprite: Graphic used to represent the object. This is what the player will see.

Object: An object in GameMaker consists of events, and sometimes a sprite to represent that object. Objects can be solid or transparent to suit your needs.

Room: This is where all of parts of your game will be. Essentially, a room is where your game will take place.

Background: This will be displayed as the background of the room. 

Sound: Sound effects and background music. By using events on an object you can make the set the sound to go off depending on the situation.

Path: By drawing a path in a room, you can set it so that an object will follow a specific path.

Timeline: Using the steps in the game, you can set it so that specific events occur at a specified time.

GameMaker on Windows is a great tool for development, with it's frequent updates and ease of going between platforms. GM on Mac, however, is better suited for prototyping and testing out features. It can still be used to make simple games, but will have less support in terms of the software itself.


<a href="#top" class="top" id="basic-top-down-shooter">Top</a>
##2.2 Basic Top-Down Shooter

We’ll be building a quick top-down shooter in GameMaker, and with the goal of seeing the features of GameMaker that combine game assets with logic to create a game. What features and commands does GameMaker have, and how are they organized in a GameMaker game? The shooter we make will be extremely basic, with enemies slowly coming down to the player’s level. You can move horizontally and shoot upwards. 

<a id="create-resource-sounds-sprites"></a>
###2.2.1 Creating Resources - Sounds and Sprites

In this section, we’ll focus on creating and adding assets to our game. When you first open GameMaker, you should see a window similar to the one in the screenshot below.
[GAME MAKER WINDOW]
The two types of assets--graphics and audio--are grouped into the first 3 folders on the left. As intuitive as the interface is, we’ll give a quick walkthrough of adding sprites, sounds, and backgrounds.

Creating a Sprite

To create a sprite, either click the pac-man icon in the top menu, or right-click the Sprites folder and select new sprite. The Sprite Properties window shows up. Name the sprite something appropriate, like sPlayer, for a player sprite. To modify the actual graphic of the sprite, you can choose to load a premade image or edit the sprite yourself and click the appropriate button. We’ve provided sample sprites with the tutorial that you can load. If you prefer to make your own, click “Edit Sprite” to open up the sprite editor and click “New Sprite”. Specify the dimensions (this applies only for Windows users), and double-click the “image 0” that’s appeared in the sprite editor.

Try to add another sprite to represent the player’s bullets! A graphic is provided.

A background is similar, and we’ve provided one. Create a background resource and load ours or draw your own backdrop for our ultimate space battle. Try to make it tile!
Sidenote: IMO GM’s sprite editor is reasonably powerful but some things are hard to find, like resizing the canvas. This is because sprites can actually contain multiple subimages of the same size, to be used in e.g., animation, or different states of an object, like a stoplight with different lights on. For professional pixel art, consider drawing in GraphicsGale or Aseprite and then loading.
The remaining options in the sprite properties dialog box have to do with how the rest of the game renders and interacts with objects with this sprite. We can get into them later.

Adding a sound

We’ve provided a sample shooting sound effect made in bfxr, and loading that as a resource is as simple as for the sprite. Creating a sound resource is a matter of navigating the interface. (Double-click the Sounds folder and clicking Create Sound, or clicking the speaker icon in the top menu. Click the folder icon at the top of the Sound Properties window to load the sprite.) For our purposes, the other settings don’t need to be changed.

Notes

One thing you might notice is that Game Maker provides a lot of options and settings to tweak for each resource. This is just because Game Maker has a lot of built-in functionality for common game use-cases, which is partly why prototyping can be really fast with GM. We avoid these settings for now as we have no use for them, but the help manual goes into them pretty well if you’re interested.

<a id="basic-game-logic"></a>
###2.2.2 Basic Game Logic

The main actors in GameMaker games are objects, which combine a sprite with game logic that is run on every step of the simulation. Objects are then placed in things called rooms, which serve as an environment for objects to interact with each other and you in a game.

A minimal program

To see how this system works, let’s create a player that can move around. First, create a new object resource (i.e., click the [BLUE BALL ICON] in the top menu or right-click the folder and select the option) and name it something appropriate, like oPlayer. Underneath the name, set the sprite to sPlayer.

Then, create a room resource. In the objects tab of the Room Properties window, select oPlayer, then click somewhere in the grid to place the player in the room (in addition, you can change the size of the grid with the SnapX and SnapY values at the top of the window). Then, in the settings tab, change the width and height to 320x480, and FPS to 60.

Now that the room’s been added, the game is minimally functional. In the top menu of the main window, click the green triangle to test the game out. Your object will be there, motionless.

Adding motion

To implement motion, we can use Game Maker’s built-in event-action functionality. Game Maker lets us program game logic into these objects by adding statements of the form, “when [EVENT], do [ACTIONS]”, like “when <spacebar> is pressed, shoot a bullet and play a sound,” or in this case, “when <left> is pressed, move left.”

To see how GameMaker provides this, in the Object Properties window of your player, click “Add Event” at the bottom, select “Keyboard” (not Keyboard press), and then “Left”. A “press <Left>” event should pop up, representing the “When left is pressed…” part of the statement. Drag the action [JUMP TO POSITION ICON] on the right to the actions window, inputting setting x to -3 and y to 0, and ticking relative, to finish the statement with a “jump to your left 3 pixels.”

Underneath the hood, GM is adding a piece of logic to the object’s programming that checks if the left button is down at a particular instant and moves left if it is. This check isn’t truly continuous because of the sequential nature of programs, but it’s as close to continuous as possible. Instead, this piece of logic is added to the object’s update method, which is run once every time step, or simulation of the game loop. This abstraction--of associating a sequence of actions to an event for every object--is relatively powerful because of the wide variety of actions and events to choose from, but also easy to work with for people inexperienced with code.

SIDENOTE: Every object has a pair of coordinates (x, y) representing its position, and GameMaker draws the sprite of the object at that position once every frame. The action we added moves the object (-3, 0) from where it was before, since we ticked relative. If we hadn’t ticked relative, the object would teleport to the absolute location (-3, 0) (i.e., a bit to the left of the origin, or top-left corner of the screen/room), and stay there, as soon as you pressed left.

[FIGURE: COORDINATE SYSTEM IN GAMEMAKER]

If you rerun the game, your player will slide to the left when you hold the left button down. Try to repeat with the other direction to give the player full horizontal mobility.

Shooting

We can continue using these event-action pairs to make the player shoot bullets, and demonstrate how objects can interact.
First, create an oBullet object and assign the sBullet sprite to the object. In the oBullet object, we add a Create event and add a [SET VERTICAL SPEED ICON] action to set the vertical speed to, say, -8, so when it spawns moves upwards. Add another event, “Outside Room”, and insert a [DESTROY] action (accessible from the main1 tab on the right) to remove the bullet once it leaves the screen (so we don’t simulate it any more than we need to).
Back in the oPlayer object properties box, add a press <Space> event (click Add Event, then Key Press, then Space) and put in there a [CREATE INSTANCE ICON] action with object oBullet, position x = 12, y = 0, and with relative ticked. We can drag another action underneath, [SOUND PLAY ICON] from the main1 tab, and select to play the shoot sound we added earlier.

SIDENOTE: The [CREATE ICON] action creates a bullet at (12, 0) relative to the player position. The way we’ve set it up, this means that the bullet we create will be placed such that its top-left corner is 12 pixels to the right of the player’s top-left corner (see the figure).

[FIGURE: creating an object at a position]

SIDESIDENOTE: If you’re interested in avoiding these ugly numbers, take a look at sprite origins, which are special coordinates for each sprite, editable in the sprite properties window. When GM renders an object at a position (x, y), it draws the object’s sprite so that the origin of that sprite is at (x, y). Sprites are created with origins at (0, 0). You can move the origin to the centre of the sprite by clicking “Center” on both the player and bullet sprites. Creating a bullet at (0, 0) relative to the player will then make the centre of the bullet align with the centre of the player, as desired. 

[FIGURE: creating an object at a position--origin centre]

<a id="object-interaction-enemies"></a>
###2.2.3 Object Interaction: Enemies

By this point adding resources should be familiar. Just as we did with the player and its bullets, we can do the same with the enemy: creating a sprite resource, loading/drawing the graphic, and creating an object resource that uses the sprite.

We’ll eventually make it so that the game periodically spawns enemies that slowly move down. One way to have the enemies move down is to program the enemies to have a downward speed upon creation: Add Event -> Create, and drag the [SET VERTICAL SPEED] action to the actions window, with a speed of 3 or so.

SIDENOTE: This is another built-in feature of GM. Every object has a horizontal and vertical speed (hspeed, vspeed), and every frame, the object’s position is shifted by the speed. Setting the vertical speed to 1 would make the object move down a pixel every frame. Ticking relative in the [SET VSPEED] action would add 1 to the current vertical speed of the object (it doesn’t matter here since the object starts out stationary). 

Another behavior we might want is to have them disappear upon hitting a player bullet. This can be done with the collision event: In the oEnemy’s Object Properties window, click Add Event -> Collision -> oBullet to include the event and drag the [INSTANCE DESTROY] action (tab main1) to the actions window. Additionally we might want the bullet to be destroyed too, which we can do by dragging another [INSTANCE DESTROY] and set the target to “Other” instead of “Self”.

If we go to the room editor and drop enemies into the room, they’ll appear and slowly move down, as well as react to our bullets, as expected.

<a id="control-flow-variables-health"></a>
###2.2.4 Control Flow and Variables: Health

GM provides a scripting language to allow for traditional control flow structures, like conditionals and loops, but GM’s drag-and-drop action system also has a simplified version for people new to code. 

Every object is allowed to have any (reasonable) number of values associated with it, called variables, that store things like numbers, pieces of text, or other objects. Their use is what you’d expect: keeping track of, e.g., an individual’s score in an arcade game, or status message in an MMO. We’ll use variables to keep track of enemy health, so that 3 hits will destroy an enemy ship instead of just one.

While there’s no explicit way to declare what variables you want an object to have up front, it’s often a good idea to set, or initialize all of them in the Create event with the [SET VAR] action in the control tab. To start the enemy off with 3 health, use [SET VAR] to set hp to 3 in the Create event. Since this is the first mention of the variable `hp`, it tells GameMaker that this object has a variable called `hp`.

NOTE: GameMaker provides a built-in global variable (i.e., not different for each object) called health for player health. I guess it’s there for people new to GM since there’s a tab dedicated to these variables (score, health, lives), but they’re no different from regular variables. We won’t be using these global variables.

In the collision with the bullet, we want to decrement `hp` and now only want to disappear if the health hits 0. To do this, we can [SET VAR] to set `hp` to -1, ticking relative. Then underneath, use a [IF VAR] to check if `hp` is equal to 0, and put the self-destruct [DESTROY] action right underneath the condition. The [IF VAR] will skip the following action unless the condition is satisfied, so the enemy ship is only destroyed if the health reaches 0. If you want a conditional item to apply to a block of events, you can use the [BLOCK START] and [BLOCK END] items to specify how far the block should reach.

[FIG: example sequence of control flow] 

<a id="alarms-periodic"></a>
###2.2.5 Alarms and Periodic Events

Enemy Fire

We can do something analogous to the interaction between player bullet and enemy with an enemy bullet. Create a sprite resource for an enemy bullet, load the graphic, and associate it with a newly created object, naming it something like oEnemyBullet. We can program the player so that the game restarts ([GAME RESTART ICON]) upon hitting an enemy bullet (or maybe after losing all its health), and then get the enemy to shoot every three seconds or so.

Perhaps the only vaguely new concept is the idea of an event happening periodically, for which Game Maker also has built-in functionality in the form of alarm events.

Alarms have two parts: an action that sets the alarm ([ALARM ICON]) and the event that’s triggered when the alarm goes off. Internally, every object has a set of built-in alarm counters. the [ALARM ICON] action sets one of the counters for an alarm. The alarm decrements every step, and when the counter reaches 0, the actions in the alarm event are triggered. For instance, to make an enemy shoot exactly one second after it’s spawned, we can use [ALARM ICON] to set the enemy’s Alarm 0 to 60 (assuming 60 FPS), and in the event Alarm 0, create an enemy bullet.
To have the enemy fire once every 3 seconds, we can have a [ALARM ICON] action setting alarm0 to 180 in both the create event and the Alarm 0 event, so that when the alarm fires, it also resets itself. In addition, in the Alarm 0 event, we create a bullet, and set the bullet to aim downwards in the bullet’s create event.

SIDENOTE: GameMaker has a bunch of scripting functions you can embed in the properties of your actions so that the engine isn’t completely restricted. For instance, we could set alarm0 to `150+random(30)` to set alarm0 to a random number from 150 to 180 every frame. The manual included with GM has a reference on all of these functions, but it’s more common to ask about or look up a certain desired behavior and learn about how GM accommodates it in an example. 

Enemy Spawning

To create a constant stream of enemies for our game, we make an object that doesn’t interact with the game at all besides creating enemies every once in a while. This pattern is common in engines where game logic is almost entirely in objects, and normally we call these background objects controller objects and use the prefix c instead of o.

Create a cEnemies (or cEnemySpawner) object without attaching a sprite, with an [ALARM ACTION] action in the Create and Alarm 0 event, along with an enemy create action in the Alarm 0 event, to produce enemies periodically.

To put the enemies at random positions, we can set the y to be -32 and x to be random(room_width-32), which generates a random number from 0 to the coordinate of the rightmost side of the room every time it’s called. This approximately evenly distributes the enemies.

SIDENOTE: The reason we set y to -32 is so that the bottom of the enemy are at y = 0, or the top of the screen, when they’re spawned. Similarly, room_width-32 is 32 pixels to the left of the right end of the room, so the farthest to the right the spawner can spawn is the position where the right side of the enemy touches the right edge of the room (the farthest to the left is x = 0, where the left end of the enemy touches the left edge of the room). 

<a id="polish"></a>
###2.2.6 Polishing up our Game

We have a half-complete prototype for our shooter. Let’s polish some of the rough edges to make it a little more presentable.

Backgrounds in Rooms
Unlike sprites, backgrounds aren’t associated with objects, but rather with rooms. To add the starry night background to the game room, double-click the game room in the left-menu to open the Room Properties window, and navigate to the backgrounds tab. Tick “Draw background color”, “Visible when room starts”, and the tiling checkboxes, and choose a color at the top and your background in the dialog box near the bottom. You can scroll down and set the vertical speed to 3 or so to make the background move down. 

SIDENOTE: Backgrounds are modifiable at any time by objects through a set of variables beginning with “background_”. Variables can be set using the [VARIABLE SET ICON] action, or through a script, which we’ll get into for the platformer, which is a step up in programming complexity.

Animations - Explosion

Precisely, sprites are made up of a set of graphics called subimages (with the same dimensions) along with other properties like a hitbox or an origin. People usually achieve animated graphics using sprites with multiple subimages and playing through the subimages.

In the Sprite Editor (to reach it, click Edit Sprite in the Sprite Properties window), one can add an empty subimage at the end of the sequence with the [SUBIMAGE ADD BTN] button and then double-click the subimage to edit it. Alternatively, one can load from a strip of subimages, like the one we provided. In the Sprite Editor, File -> Create From Strip opens a dialog box that extracts subimages from a sheet of images. Our sprite sheet has 7 images and 7 images per row, with all other settings unchanged. To see how the animation plays out, you can tick the “show preview” checkbox in the Sprite Editor. 

Using our animated sprite is a matter of making a new object and assigning the explosion sprite to it. The single behavior to add to the explosion object is a [DESTROY] to itself when the animation ends, accessible from Add Event -> Other. Other objects like the enemy can create explosion objects in the event of hitting a player bullet.

Other

There are a lot more things that could be done to make the game more presentable, like restricting the player from moving outside of the screen, which can be done by only allowing rightward movement if the player `x` is less than `room_width-32`, and only allowing leftward if the player x exceeds 0. 
One other thing you may notice is that the game isn’t fun. Try to tweak the game to make it challenging! Make the game restart when an enemy reaches the bottom of the screen. Change the enemy bullet pattern, perhaps aiming at the player instead of downwards (use [MOVE FREE] in the bullet create event, with direction `point_direction(x, y, oPlayer.x, oPlayer.y)`). Get the enemies to move horizontally too, bouncing against the sides of the room, or add your own gimmick after exploring the actions GameMaker has.  


<a href="#top" class="top" id="MVP-review">Top</a>
##2.4 Let's Review Level 2!

Game Maker tries to make it simple to make simple games. Where there isn’t a lot of complex logic, programming and gathering the assets is a matter of navigating the menus and specifying what to do at certain events. 

GM is powerful too, though, with many layers of complexity underneath. Logical control flow in an object can get complicated too with conditionals and variables to manage. GM also has a scripting language that lets you implement complex behaviors as well as bypass the built-in crutches provided for the beginner.

While it would be a chore to go through the enormous list of functions and actions GM provides, there are many tutorials online for specific behaviors. As you go through examples, you’ll naturally pick up and learn how each useful function/action is used in games.

In the next tutorial, we’ll go through the scripting capabilities of Game Maker and look at some more general considerations in game programming.

___________
<a href="#top" class="top" id="level3">Top</a>
##Level 3: Making a Platformer

In this platformer tutorial we’ll take a different approach with GM, instead limiting ourselves to just a few of the built-in features related to resources and coding the rest ourselves, to get a feel for how GameMaker works underneath the event-driven model (and how game engines in general work), and look a bit at some of the problems games programmers face in implementing mechanics.

This section in particular will be a little more math-oriented as we figure out how to get our player to behave and move exactly how we want. 

<a href="#top" class="top" id="resource-setup">Top</a>
##3.1 Resource Setup

Create and load the player and enemy sprite, as well as the background tileset, checking “Use as tileset” in the properties. Alternatively, draw your own if you feel brave, but try to keep the poses similar and the image dimensions 16x16. In addition, create a 16x16 black square to represent the blocks our player is going to interact with, and create the corresponding oBlock object. The black sprite box is just for the level editor and won’t be what the player sees, though; we’ll cover the blocks up later with a tileset to make it visually pleasing. 

<a href="#top" class="top" id="scripts-step-events">Top</a>
##3.2 Scripts & the Step Event

<a id="step-event"></a>
###3.2.1 The Step Event

Game Maker exposes the update method of every object through the step event. That is, actions in the step event are run every frame the object exists. Most, if not all event action pairs could be reduced to a set of actions in only the step event. For instance, you could have an enemy disappear upon hitting your bullet by using the [CHECK COLLISION ICON] against the bullet and following that with a [DESTROY ICON] in the enemy’s step event. The logic is the same: “When I hit a bullet, destroy myself” is the same as “At each frame, if I am hitting a bullet, destroy myself.” Again, the emphasis with these patterns is the continuous repetition of blocks of code that may be deficient in traditional sequential programs.

<a id="GM-language"></a>
###3.2.2 The GameMaker Language

[screenshot]

In the control tab, Game Maker provides the [EXECUTE CODE] action, which really opens up the full functionality of the tool by giving access to all the programming functions. The code editor has tooltips as well as syntax checking and highlighting. The language itself is C-like, but without explicit type (ints, doubles, strings default) and more merciful of traditional syntactic errors (e.g., code will compile without a semicolon; you can do things like `if (x = 5)`). There are a few things that someone with a programming background might cringe at, but I personally think the conveniences GM provides (in the form of resource management, collision detection, room editing, built-in variables, etc.) outweighs any sort of annoyances in GM’s code interface.

[SAMPLE CODE/IMAGE OF CODE EDITOR]

With these two tools, we can reduce any object behavior to a single [EXECUTE CODE] action in the step event, and possibly another in the create event (for setup) and destroy event (for cleanup). However, it’s still useful to divide logic into different events and actions if possible, if only just to better organize and clarify the object’s behavior.

<a id="GM-defaults"></a>
###3.2.3 The GameMaker Defaults

Game Maker has a bunch of options that might look relevant here, like “Uses Physics” (windows only) or “Solid” in the Object Properties window. One of them uses a powerful 2d physics engine, but it’s overkill for our purposes. The other is a very naive collision system that would result in an annoying, broken platforming engine. You would be sad.

<a href="#top" class="top" id="horizontal-movement">Top</a>
##3.3 Horizontal Movement

We’ll start by giving the player the ability to move left and right.

<a id="first-attempt"></a>
###3.3.1 A First Attempt

For instantaneous speed, we can add the following piece of code to the step event of the player:

CODE:
if (keyboard_check(vk_left))
x -= 4;

if (keyboard_check(vk_right))
x += 4;

That is, in each frame, the program checks if the left key is pressed or not. If it is, the player jumps to the left 4 pixels. Analogously for the right key. To be precise, keyboard_check(...) is a function provided by GM taking in a key code and outputting whether it’s down or not. 

If you put the player in a room (appropriately set up) and run the game, you’ll see that pressing left moves the player left and right right. 

<a id="smooth-movement"></a>
###3.3.2 Smooth Movement

Most platformers consider player acceleration and deceleration. In a smooth platforming engine, we’d expect pressing a horizontal to gently accelerate the player in that direction up to a maximum speed, releasing that direction to slowly decelerate the player, and pressing the opposite direction to shift towards that opposite direction. 

We can model this using two speeds--a rightward speed and a leftward speed--each individually controlled by the corresponding key.

To define and initialize object member variables, we can simply assign values to them in the Create event: 

/// initialize variables
rspeed = 0;
lspeed = 0;
accel = 0.1;
maxspeed = 3.5;

(Putting 3 slashes in the first line replaces the default “Execute Code” action description with the text of the first line)

SIDENOTE: The object-oriented mind may notice that even though the last two variables are actually constants (at least, for our purposes) specific to all player objects, it’s common practice to group these with other member variables. This may be a little unsettling, but it’s the best solution given GM’s restricted capabilities (AFAIK). Further, the idea and purpose of an object in games are slightly different than in traditional OOP use-cases; these represent packages of code that are simulated according to a ruleset, not possible interfaces or services for other users or other classes, and the people who do work with your object’s code are much less likely to want to break it. Magic numbers are still bad for the same reasons as in other programs, so we define variables here.

To have the right key control rspeed and the left control lspeed, we put, in the Step event:

CODE:
if (keyboard_check(vk_right)) rspeed += accel;
else rspeed -= accel;
if (keyboard_check(vk_left)) lspeed += accel;
else lspeed -= accel;

We can then restrict the two speeds by appending:

CODE:
if (rspeed > maxspeed) rspeed = maxspeed;
if (rspeed < 0) rspeed = 0;
if (lspeed > maxspeed) lspeed = maxspeed;
if (lspeed < 0) lspeed = 0;

(Would it matter if this second block were placed before the first? Try it out, and think about what happens, if anything happens at all, keeping in mind that this is just code that’s run once per frame)

And finally, append hspeed = rspeed - lspeed. GM automatically does x += hspeed at the end of every step (if that’s not your thing, write xspeed = rspeed - lspeed and do x += xspeed yourself).

If you rerun the game, you’ll notice that while we haven’t done anything fancy to simulate physical forces like friction or drag, the player’s movement is a lot smoother and closer to the movement mechanics of, say, Super Mario Bros, or Spelunky.

<a href="#top" class="top" id="vertical-movement">Top</a>
##3.4 Vertical Movement

The vertical movement in a platformer is governed by gravity, which is usually a constant downwards acceleration. In addition to that, the player should be able to jump. For this section, we’ll add gravity but no ground, and instead give the player the ability to jump in the air.

<a id="gravity"></a>
###3.4.1 Gravity

A constant downward acceleration translates to a continuous addition of downward speed. We can do this by defining `grav = 0.5` in the Create event and then `vspeed += grav` in the Step event.

<a id="jumping"></a>
###3.4.2 Jumping

Jumping is usually an upward burst of motion. We can implement jumping with another constant in the step event, `jumpspeed = 6`, and a simple key check in the Step event:

if (keyboard_check(vk_up)) vspeed = -jumpspeed;

SIDENOTE: Though we’ll eventually make it so that the player can only jump if it’s on the ground (i.e., vspeed is 0 initially), in games with multiple jumps, the player’s second jump isn’t affected by how the player’s moving before the second jump, so we say `vspeed = -jumpspeed` instead of `vspeed -= jumpspeed` (of course, this is all up to how you want jumping to work in your game).

<a id="stopping-your-jump"></a>
### 3.4.3 Stopping Your Jump

Often in platformers, one can control the player’s jump height by releasing the jump key early or late. There are many ways to implement this underneath. For instance, one could halve the player’s upward velocity when the jump key is released:

if (vspeed < 0 && keyboard_check_released(vk_up)) vspeed /= 2;

Or, for a smoother motion, consider applying a stronger gravity while the player’s moving upwards if the jump button isn’t pressed:

if (vspeed < 0 && !keyboard_check(vk_up)) vspeed += grav2; else vspeed += grav

SIDENOTE: GM does not have the conditional operator (a ? b : c). Sorry.

<a id="walking-animation"></a>
###3.4.4 Walking Animation

If you loaded all 4 subimages of the player sprite, you might want to have the player animation correspond to your movement. The variables GM provides to control the displayed subimage of a sprite are `image_index`, the subimage index, and `image_speed`, the speed at which image_index changes. A speed of 1 means every frame, the index advances; ½ would mean updating the subimage once every two frames.

If we wanted to have the animation play at a speed according to how fast we were moving, we might do something like `image_speed = 0.05*hspeed`.

To get the player to change the direction he’s facing, a common solution is to create another sprite with the graphics mirrored and then set the player’s sprite according to his speed, using GM’s built-in variable `sprite_index`. Something like

CODE:
if (hspeed >= 0) sprite_index = oPlayer;
else sprite_index = oPlayerL;

SIDENOTE: Alternatively, GM provides variables image_xscale and image_yscale, which, as the names suggest, define how the sprite should be scaled when it’s rendered. Normally, they’re set to 1, but having image_xscale = 0.5 would squish the sprite so its width were half what it is usually. Setting it to a negative value flips the sprite, so when moving left, we can set `image_xscale = -1` to face the player left. The complication with this is that this is literally scaling with respect to the origin of the player sprite, so if we flipped the sprite, the box would teleport to the left 16 pixels (see figure). We want to put the origin somewhere so that if we flip the sprite, the image doesn’t shift any amount (see figure). This happens when the origin’s x is centred (i.e., origin is at (8, 0)).

[FIGURE: flipping] [FIGURE: origins and flipping right]

A slick (and/or disgusting) way to do it is this line in the Step:

if (hspeed != 0) image_xscale = sign(hspeed);

<a href="#top" class="top" id="platform-collision">Top</a>
##3.5 Platform Collision

This is the more technically challenging part of platformer physics: determining collision detection and response. Roughly, we want to implement a statement like “If the player hits a block, stop the player from moving into the block and set his velocity accordingly.”

This encompasses a lot of cases. What should happen if the player hits the bottom of a block? What if he lands on a block? Or if he hits the side of a block? And what about if he hits the exact corner of a block?

A simple observation we can make is that unless we want to add friction or wall-sliding, a player hitting the side of a block only affects it his horizontal velocity, and a player hitting the top or bottom of a block only affects his vertical. We can therefore try to approach the two directions separately.

The relevant set of functions is instance_place(x, y, other) and place_meeting(x, y, other), which check if an object `this` calling place_meeting would touch `other` if `this` were moved to position x, y. This is equivalent to moving `this` to (x, y), then checking if the hitboxes (as defined by the sprites of the two objects) overlap, and then moving `this` back to its original position. instance_place returns the object that may be touching (or else noone), and place_meeting returns whether or not there’s an object touching. We’ll give some examples to clarify. 

<a id="landing-block"></a>
###3.5.1 Landing on a Block

Recall that update methods and the game loop try to simulate a ruleset for the universe of our game by running a block of code almost continuously--once every frame. We can’t enforce the statement, “Don’t let the player fall through a block when he lands on it” directly, but we can ask each frame if he’s landed on the block, and if he has, change the player’s motion and position accordingly. 

The way we can do this with GM is to check, in the update method, whether or not the player would fall into a block the next frame. This is a matter of moving the player to where it would be next frame, and seeing if the player’s hitbox in that position overlaps with the block’s. This can be captured with the condition `if (place_meeting(x+hspeed, y+vspeed, oBlock))` at the end of the other movement code, because the player’s position next frame is (x+hspeed, y+vspeed). If the condition passes, we know that unless we do something, next frame, the player will be stuck in a block.

SIDENOTE: Why wouldn’t this condition work if it were placed at the beginning of the step event? 

What we need to do is twofold:

1. Stop the player from continuing to fall by setting the vspeed to 0.
2. Reposition the player so that next frame, instead of being inside the block, he’s instead right on top of the block. 

[FIGURE: frame 1, frame 2 player on block, X frame 2 player overlap block, moving down]

To determine how to reposition the player, consider the figure, which labels the origins of the player and the block. We want the bottom of the player to line up with the top of the block, and in order to do that, the player’s origin must be 16 pixels (the player sprite height) above the block’s.

[FIGURE: PLAYER ON TOP OF BLOCK, LABELS, GRID]

`y = (y position of the block i’m touching) - (sprite height)`

SIDENOTE: If you moved the origins of the player and block around, it’s a little more complicated, but doable with the instance variables sprite_xoffset and sprite_yoffset. 

[FIGURE: PLAYER ON TOP OF BLOCK, SPRITE_YOFFSET, LABELS]

`y = (y of block i’m touching) - (sprite_height) + (sprite_yoffset) - (y of block i’m touching’s sprite_yoffset)`

SIDESIDENOTE: If in addition, you resized the hitboxes, you may need to avoid hard-coding the hitbox offsets or use a different approach, as GM doesn’t provide hitbox dimensions and offsets (it doesn’t work if the sprite hitbox setting were elliptical, or pixel-perfect). One way may be to use a loop to nudge the player upwards until he doesn’t overlap with the block anymore, but it would have to be carefully written so that the player doesn’t get nudged over the edge of the block.

To summarize, we have the following block of code to make the player behave appropriately when he’s about to fall onto a block:
z = instance_place(x+hspeed, y+vspeed, oBlock);

CODE:
if (z != noone) {
    vspeed = 0;
    y = z.y - abs(sprite_height);
    // or z.y - abs(sprite_height) + abs(sprite_yoffset) - abs(z.sprite_yoffset)
}

NOTE: sprite_width, sprite_height, sprite_xoffset, and sprite_yoffset are multiplied by image_xscale and image_yscale, so e.g. if the sprite had size 16x16 and the origin were at (8, 0), and image_xscale were -1, sprite_width would be -16, and sprite_xoffset would be -8. This is why we put an absolute value.

To keep it so that the player stays on the block, we can just put this block of code just under the line that applies gravity. If the player is already on the block, each frame will try to apply gravity but then instantly negate it.

<a id="hitting-block-bottom"></a>
###3.5.2 Hitting a Block from the Bottom

If you put a few blocks in the room and test the game out, you’ll notice that no matter which direction you hit the block from, the player will always teleport above the block. We’ll now cover the other vertical direction.

But how can our code tell if the player hit the block from the top or bottom? Our current code simply checks for an overlap and puts the player on top of the block if there is. A few solutions:

1. Assuming the player isn’t currently overlapping with the block, if the player would hit the block next frame, the player must be hitting the top of the block if he’s moving down (vspeed > 0) and the bottom if he’s moving up (vspeed < 0).

2. We can just check if the player is above (y < z.y) or below (y > z.y) the block.

If we want to add more functionality in the future we should use the second method, as it more directly relates to the question we’re asking. What if we want to add moving platforms later that cause a hitbox overlap? If the player’s moving up while on top of the platform, the first check would fail.

As with landing on a block, we want to set the vspeed to 0 so the player doesn’t phase through the block. To find where to reposition the player to, it may be helpful to make a figure:

[FIGURE: player under block]

In this case, the top of the player intersects with the bottom of the block. We use:

y = z.y + abs(z.sprite_height) \\ - abs(sprite_yoffset) + abs(z.sprite_yoffset)

Our final vertical collision code is

CODE:
z = instance_place(x+hspeed, y+vspeed, oBlock);
if (z != noone) {
    vspeed = 0;
    if (z.y > y) y = z.y - abs(sprite_height) + abs(sprite_yoffset) - abs(z.sprite_yoffset);
else y = z.y + abs(z.sprite_height) - abs(sprite_yoffset) + abs(z.sprite_yoffset);
}

<a id="hitting-block-side"></a>
###3.5.3 Hitting the Side of a Block

When the player hits the side of the block, he should stop all horizontal movement, both left and right, and be repositioned so he is next to the block.

[FIGURE: player hitting side, grid, labels]

Following the figures above, we get the following block of code for the step event:

CODE:
z = instance_place(x+hspeed, y+vspeed, oBlock);
if (z != noone) {
    hspeed = 0;
lspeed = 0;
rspeed = 0;
    if (z.x > x) x = z.x - abs(sprite_width) + abs(sprite_xoffset) - abs(z.sprite_xoffset);
else x = z.x + abs(z.sprite_width) - abs(sprite_xoffset) + abs(z.sprite_xoffset);
}

Replace the vertical collision detection code with this to see the player react horizontally upon touching a block.

<a id="horizontal-verticle"></a>
###3.5.3 Horizontal or Vertical Collision?

If you put both chunks of code in after the regular motion portion of the step event, you’ll notice that only the first chunk affects the player’s movement. This is because both checks are the same, and the first check moves the player out of the way of the block. By the time we reach the second check, there’s no block to react to, and thus no further adjustment is made.

[Spoiler: To fix this, one can just change the check in the first chunk of collision code from (x+hspeed, y+vspeed) to either (x+hspeed, y) if the first check is the horizontal adjustment, or (x, y+vspeed) if vertical. To see why, see below]

We need our code to decide whether a given collision is vertical or horizontal. One way is to compare the relative positions of the block and player, as we did to see if a collision was on the top or bottom.

[FIGURE: dividing a block + surroundings into 4 quadrants to see which side you’re touching]

But this is a hassle as the player collides closer and closer to a corner of the block, especially if the player’s origin or hitboxes are shifted. Instead, we can make two other checks: collision against the block at (x+hspeed, y), and at (x, y+vspeed), visualized below.

[FIGURE: 3 checks for player]

If the player is going to be hit a block from the side, the player will most likely intersect the block if the player moves to position (x+hspeed, y).

[figure]

Then we can react with our horizontal collision code in this case. Similarly if the player is going to hit a block from the top or bottom, there’ll probably be an intersection for (x, y+vspeed) and we can apply vertical collision there.

[figure]

If the player hits from a corner, though, neither of the two checks will report a collision, and nothing will be done. Our player will end up in a block. This case is extremely rare for any platformer with a reasonable resolution/framerate, and requires a very precise jump. In this case, we can apply either horizontal or vertical correction. We’ll be nice and put the player on top (or bottom) of the block if he meets the block at a corner. 

A summary of our code:

CODE:
if (hit block at (x+hspeed, y)) apply horizontal correction;
if (hit block at (x, y+vspeed)) apply vertical correction;
if (hit block at (x+hspeed, y+vspeed)) apply vertical correction;

A simplification would be to remove the second line entirely, since the second line rarely fires without the third also firing--only when the player grazes the block from the top almost pixel-perfectly.

[Figure: player grazing from top]

Our final code:

CODE:
z = instance_place(x+hspeed, y, oBlock);
if (z != noone) {
    hspeed = 0;
    lspeed = 0;
    rspeed = 0;
if (z.x > x) x = z.x - abs(sprite_width) + abs(sprite_xoffset) - abs(z.sprite_xoffset);
else x = z.x + abs(z.sprite_width) - abs(sprite_xoffset) + abs(z.sprite_xoffset);
}

z = instance_place(x+hspeed, y+vspeed, oBlock);
if (z != noone) {
    vspeed = 0;
    if (z.y > y) y = z.y - abs(sprite_height) + abs(sprite_yoffset) - abs(z.sprite_yoffset);
else y = z.y + abs(z.sprite_height) - abs(sprite_yoffset) + abs(z.sprite_yoffset);
}

<a id="jump-right=time"></a>
###3.5.4 Jumping at the Right Time

At this point we can restrict the player so he can only jump if he’s touching the ground. We can replace our current jump line with something like

if (keyboard_check_pressed(vk_up) && place_meeting(x, y+1, oBlock)) vspeed = -jumpspeed;

so that the player is only allowed to jump if he’s on the ground (i.e., a block sits at most one pixel below him).

<a id="optional-quirk"></a>
###3.5.5 Optional: A Quirk with GM

(This happens in the latest version of GM studio on Windows. Not sure about earlier versions. Feel free to scroll to the bottom for the solution.)

If you look carefully, you might see your player vibrate as he stands (especially if you’re zoomed in). This is especially obvious if you have him move left against a wall and watch him turn. This is sadly a small problem with GM’s collision detection: it does rounds down object coordinates before checking in instance_place. 

Over the course of two game loops, the player moves from right above the block to slightly inside the block and back out. The first movement is because the player is pulled down slightly from gravity, over less than a pixel. GM does the collision check, testing the player’s original position (because of rounding down), and sees that nothing’s there, even though we can clearly see the player overlapping with the block. From this position, moving another few fractions of a pixel down would put it over a pixel beneath its original position, and GM detects that, moving the player back to right above block.

[FIGURE: player overlapping and then moving back and then overlapping]

We have no avenue to get GM to test fractional positions, but we don’t need to if we round the positions we test ourselves to make sure we’re testing the right spots. For instance, in the case described above, this wouldn’t be a problem if GM rounded up. In general we’d like to round up if the player’s moving right/down, and down if the player’s moving left/up. Define a few variables:

CODE:
var xrounded; if (hspeed > 0) xrounded = ceil(x+hspeed); else xrounded = floor(x+hspeed);
var yrounded; if (vspeed > 0) yrounded = ceil(y+vspeed); else yrounded = floor(x+vspeed);

SIDENOTE: For variables local to the event, you can prepend the variable initialization with `var`.

Then use them in the collision code:

CODE:
z = instance_place(xrounded, y, oBlock);
if (z != noone) {
    hspeed = 0; lspeed = 0; rspeed = 0;
    xrounded = floor(x);
if (z.x > x) x = z.x - abs(sprite_width) + abs(sprite_xoffset) - abs(z.sprite_xoffset);
else x = z.x + abs(z.sprite_width) - abs(sprite_xoffset) + abs(z.sprite_xoffset);
}

z = instance_place(xrounded, yrounded, oBlock);
if (z != noone) {
    vspeed = 0;
    if (z.y > y) y = z.y - abs(sprite_height) + abs(sprite_yoffset) - abs(z.sprite_yoffset);
else y = z.y + abs(z.sprite_height) - abs(sprite_yoffset) + abs(z.sprite_yoffset);
}

This concludes our main platforming engine section. Hopefully it didn’t seem like just a list of magical steps, but instead a case study in breaking a problem in simulation down to simpler steps. Of course, we omitted a big part of the process: testing and experimentation, figuring out what’s wrong at each step. A platforming engine is hard to make on your first try, and even on your n-th try, because there are so many cases to consider and bang your head over.

We head back to a few more common concepts in game programming.

<a href="#top" class="top" id="views">Top</a>
##3.6 Views

Our screens are only so big, and for longer levels we can’t possibly have the game window stretch to fit everything. For this reason we have views, which define a small rectangle in the room that our game window is able to see. Platformer levels are normally huge, with the window often only seeing a 320x240-pixel frame of it. This is usually zoomed up so that the actual program window size, or view port, is, say, 640x480 or 960x720. To avoid a blurry image from upscaling, go to “Global Game Settings” in the left menu -> Windows -> Graphics, and uncheck Interpolate Colors between PIxels.

[FIGURE: large level, small view window]

To achieve this, go to the Room Properties and then the view tab. Enable the use of views, and make the zeroth view visible when the room starts. Finally, to match the figure above, set the width and height of the view in room to (320, 240), along with the view port to (640, 480), to match the figure above.

[view settings interface]

If you test it right now, you’ll notice you can only see the leftmost end of the room, and the player can easily move out the right side. We want this frame to follow the player, and GM provides an option for that right underneath the rest of the view settings. You can select to follow the player and adjust the Hbor and Vbor to set how close to the edges of the view the player’s allowed to be. Hsp and Vsp define how fast the view is allowed to move to catch up to the player if the player moves too close to the edge (-1 is a special number to mean instantaneous).

If you don’t prefer the instant update, maybe it’d be helpful to create a view controller object that smoothly follows the player, and then have the view center on the controller.

(Gamasutra has a great survey of a lot of different view motions in platformers and other video games here)

<a href="#top" class="top" id="tiles">Top</a>
##3.7 Tiles

Common practice with GM and other 2D level editors is the use of a tileset, which has many parallels to a background: just an image without any complex behavior. Tile layers are images covering the room made up of unit images called tiles.

If you loaded the tileset provided as a background and marked it to be used as a tileset, it should be available in the tiles tab in the Room Properties window. You can then select it, pick tiles, and place them in the room over the blocks. If nothing seems to happen, it’s likely because the blocks are showing up in front of the tiles. You can change the rendering order by changing the layer the tiles are on (bottom of the left tile-selection menu); lower layers are rendered first. 

For relatively static environments, tiles are a good way to separate function from appearance. One can make a level by laying out the blocks and important objects, and then adding the decorative tiles to serve as background or a face for the blocks. It may also be useful to, in the oBlock’s object properties, uncheck the “visible” box.

<a href="#top" class="top" id="additions">Top</a>
##3.8 A Few Additions

We’ll finish with a quick look at adding a particular type of enemy and coins. These are short add-ons, and the nature of this section of the tutorial generally reflects the general experience with Game Maker: an idea/desire for a gimmick/feature, leading to looking up a short tutorial online, leading to a little more awareness of GM’s features and how to use them, as well as some intuition for general game programming.

<a id="enemies"></a>
###3.8.1 Enemies

We’ll go over how to implement a Goomba-like enemy: a slow walking figure that turns around upon hitting a wall or edge and that the player can stomp on. Start by creating the object from the sprite.

MOVEMENT:

If we aren’t expecting to subject our enemy to complicated physics, we can have the enemy move horizontally, and reversing direction upon hitting a wall.

What about cliffs? We could also have the enemies detect the edge of the platform themselves, but perhaps the simplest solution for simple enemies and platforms would be invisible blocks that interact only with enemies, signalling to them that it’s time to turn around. They could then be placed strategically at the edge of platforms. 

We might end up with something like `hspeed = -0.25` in the Create event and in the Step event:

CODE:

if (place_meeting(x+hspeed, y, oBlock) || place_meeting(x+hspeed, y, oEnemyBlock)) hspeed *= -1;

COLLISION:

How do we tell if a given collision between the enemy and player is a stomp or not? Two common ways: comparing the heights of the two objects, and looking at the velocity of the player.

The former might look like something in the player Step event, above the line that applies gravity:

CODE:

z = instance_place(x, y, oEnemy);
if (z != noone) {
    if (z.y - 5 > y) {
        with z { instance_destroy(); }
        vspeed = -jumpspeed/2;
    }
    else instance_destroy();
}

NOTE: with <object> { … } runs a block of code as if that object were running it. For instance, accessing x in this block would get <object>’s x.

Super Mario Bros. actually just checks if the player’s falling, with the condition (vspeed > 0) instance of (z.y - 5 > y). You should test out what feels right.

DEATH ANIMATION:

To make the interaction less rough, we might want to add a death animation for the enemy, perhaps by having the enemy fall off the screen. A common way to do this is to replace the enemy with a different, identically-looking object with the sole purpose of falling off the screen, rather than keeping track of whether or not the enemy’s dead.

<a id="coins"></a>
###3.8.2 Coins

Another common element in platformers are mass collectibles, like coins in Mario, bananas in Donkey Kong, or rings in Sonic, and with a little extra code, can make a nice effect.

One way to add coins: Load the sprite, and create oCoin and oCoinCollect, so that oCoin disappears and changes into oCoinCollect upon touching the player. oCoinCollect can then slowly move up and fade out, destroying itself upon disappearing.

A way to keep track of coins may be to create an object just for coin counting and other game-global variables, like cCounter, and then increment the counter on that (e.g., cCounter.coins += 1, but first initialize coins to 0 in the Create event of cCounter) for every new coin collected. We haven’t gone through manually displaying text or graphics, but it’ll be covered in the menu section.


___________
<a href="#top" class="top" id="level4">Top</a>
##Level 4: States and Menus

<a id="states"></a>
### 4.1 What are they?

A finite state machine is an abstract model that can represent a program. In the machine are states, and at certain states the machine will perform a different action based on the input it receieves. Based on the input, the machine can move to another state, where it will follow a different set of rules than the previous one. (Taking the class Computer Science Theory will let you get more in-depth with FSM, along with other models of computation!)

<a id="another-subsection"></a>
###4b Application in games?

In a way, a game is a very elaborate computer program, and as such the idea of a FSM can come in handy when planning out your game. The states in an FSM can be seen as different scenarios in your game, and in different scenarios, ideally different things should happen. Thinking of the player's choices as inputs, at different scenarios you would want the game to make choices based on those inputs. 

<a id="another-subsection"></a>
###4c How does GM's rooms give this functionality?

The rooms in GameMaker can be seen as a state. The player will give the inputs, and depending on what room that the game is currently on will determine the outcome of those inputs. A room in GM have specific properties that will determine the outcome of a player's actions. For example, in a room with heavier gravity than the previous room will cause the player's jump height to be lower. Moving between rooms can also be seen as moving between states. Many things, like score, lives, and the like can determine which room will be the next room that the player will go to.

<a href="#top" class="top" id="additionalresources">Top</a>
##4b

<a href="#top" class="top" id="additionalresources">Top</a>
##4c

<a href="#top" class="top" id="level5">Top</a>
##Level 5: Design considerations: What will make your game stand out from the crowd?

Congratulations! You made it to the end of this lesson! Now that you have made two games, and have gotten a feel for game design, why don't you start embellishing these games to make them truly stand out? We don't go step by step for these suggestions, but we'll give helpful hints to guide you.

Now, here are some gimmicks you can try to add into your game!

Power-up items: Remember how we added coins in our platformer? Adding items is probably the next thing that came into your mind. Adding an item is very similar to adding a coin into your platformer, and the effect they have can be determined by you! Just like how we wrote how to make the coin counter go up as you collected more coins, you can code in specific effects, like the player getting larger or becoming invinsible, as well.

Gaining extra lives based on some value: Have you played Super Mario Bros.? If you have, you would probably know that collecting 100 coins nets you an extra life. Why don't you try adding that in to your game? But, it doesn't have to necessariliy be the number of coins. Why not have it so that for every 1000 points in your score you get an extra life? Try to get creative here! And why an extra life? Why not make it that the player becomes invincible? Or super big? Or anything really that you can come up with!

Special platforms/spaces: Now that you know that everything in a room in GameMaker is an object, why not play with that idea and try to make special platforms or spaces? How about a space that makes the player super fast for a few seconds? Or maybe a spring to let them jump higher? By making special space objects and adding events to either the player or the space itself to give these effects can help make your platformer more dynamic and open up new revenues for in-game puzzles and more creative level designs!


The possibilities are endless when designing a game. This is a world you're creating, so don't be afraid to experiment when making it! 
___________



<a href="#top" class="top" id="additionalresources">Top</a>
## Additional Resources

Along with this tutorial, there is a wealth of information available on Python all across the web. Below are some good places to start:

- [ADI Resources][learn]
- [Codecademy][codecademy]



[github]: https://github.com/yuxshao/learn-gamedev.git
[learn]: http://adicu.com/learn
[codecademy]: http://www.codecademy.com
[adi]: http://adicu.com
 
