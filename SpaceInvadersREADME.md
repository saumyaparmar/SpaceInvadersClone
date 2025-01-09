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
