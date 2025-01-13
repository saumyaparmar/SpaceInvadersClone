# Welcome to the Space Invaders Clone repository!!! 🚀👾

Get ready to defend Earth from waves of relentless alien invaders in this nostalgic remake of the classic arcade game, Space Invaders! 
In this project, I’ve recreated the iconic space shooter played in an arcarde, preserving the original’s intense gameplay and adding some exciting enhancements along the way.

This project is made as a project for my Grad Class. It is created using a custom 2d game engine by my professor. This repository will explain
how I have used more than 10 different code design patterns to create this game. I have coded this using C# language, using irrklang for sound integration.

## Features:
+ Classic Space Invaders gameplay
+ 2 Levels of alien waves
+ Increasing speeds with kills
+ Destructible shields and laser fire
+ High-score tracking to challenge your friends (or yourself)
+ Simple, clean UI

# 👾 Demo 👾

![GifSpaceInvaders](https://github.com/user-attachments/assets/83e0adbc-a4b7-49ea-be6b-01bff528892c)


# CODING PATTERNS USED 

+ Observer
+ Factory
+ Proxy
+ Command
+ State
+ Composite
+ Strategy
+ Visitor
+ Iterator
+ Object Pools
+ Singleton
  and many more...


# System Architecture of Creating Space Invaders Clone

I have made this game using a custom 2D Engine created by my professor. It provides a system to add Sprites and render it.
Sprites are a two-dimensional image used to represent a character, object or anything. Space Invaders contains various types of objects which are added as sprites.

Space Invaders contains 4 types of enemy types Octopus, Squid, Crab and at random event an UFO. There are four shields, one SpaceShip used to shoot the aliens.
There are also many others sprites which are used in Space Invaders.

To load and manage all these sprites, I have created a architecture using different design patterns. 

# MANAGER OF NODES (OBJECT POOLING)

A Node is the linked list data type which contains data and points to the next node in the list. To manage different types of data such as Sprites, Images, Textures, etc. It needs a manager which can manage its creation as well as its deletion of these data types.

So I have created a manager of nodes in a single linked list or a double linked list.
![image](https://github.com/user-attachments/assets/d8351975-9ae2-4a74-bb01-ec2382dee2a3)



This is the UML diagram of the classes and how they are connected. This is manager which manages a single linked list nodes. I can swap the SLink and SLinkMan with DLink and DLinkMan respectively for managing double linked list nodes.

Now, here the ManBase manages a reserve and active pool of nodes required at certain time. This pattern as you can see is called Object Pooling.

Challenge: Creation and Destruction of objects, especially in large numbers or in a rapid succession.
As there is a frequent need of creating and destroying instances, like gameobjects, sprites. Constantly creating and destroying these instances can lead to slowing down the system and cause performance issues.

The object pooling pattern solves this problem by creating a set of initialized objects—known as a "pool"—and then traversing through them, reusing objects from the pool rather than creating new ones. When an object is no longer needed, it is not destroyed, it is resetted and returned to the pool for future use.

