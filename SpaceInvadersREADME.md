# Welcome to the Space Invaders Clone repository!!! 🚀👾

Get ready to defend Earth from waves of relentless alien invaders in this nostalgic remake of the classic arcade game, Space Invaders! 
In this project, I’ve recreated the iconic space shooter played in an arcarde, preserving the original’s intense gameplay and adding some exciting enhancements along the way.

This project is made for my Grad Class. It is created using a proprietary 2d game engine by my professor. This repository will explain
how I have used more than 10 different code design patterns to create this game. I have coded this using C# language, using irrklang for sound integration.

This here is the detailed document about the design patterns used in creation of this game clone.

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

I have made this game using a custom 2D Engine created by my professor. Engine provides a system to add Sprites and render it.
Sprites are a two-dimensional image used to represent a character, object or anything. Space Invaders contains various types of objects which are added as sprites.

Space Invaders contains 4 types of enemy types Octopus, Squid, Crab and at random event an UFO. There are four shields, one SpaceShip used to shoot the aliens.
There are also many others sprites which are used in Space Invaders.

Here is how I have used different design patterns to create my game architecture...

# 1. MANAGER OF NODES (OBJECT POOLING PATTERN) 

A Node is the linked list data type which contains data and points to the next node in the list. To manage different types of data such as Sprites, Images, Textures, etc. It needs a manager which can manage its creation as well as its deletion of these data types.

So I have created a manager of nodes in a single linked list or a double linked list.
![image](https://github.com/user-attachments/assets/ce30da4c-aefc-4baa-b830-28b5bfe5cff7)




This is the UML diagram of the classes and how they are connected. This is manager which manages a double linked list nodes. I can swap the DLink and DLinkMan with SLink and SLinkMan respectively for managing single linked list nodes.

Now, here the ManBase manages a reserve and active pool of nodes required at certain time. This pattern as you can see is called Object Pooling.

Challenge: Creation and Destruction of objects, especially in large numbers or in a rapid succession.
As there is a frequent need of creating and destroying instances, like gameobjects, sprites. Constantly creating and destroying these instances can lead to slowing down the system and cause performance issues.

The object pooling pattern solves this problem by creating a set of initialized objects—known as a "pool"—and then traversing through them, reusing objects from the pool rather than creating new ones. When an object is no longer needed, it is not destroyed, it is resetted and returned to the pool for future use.

1. Pool Manager (ManBase and SpriteGameMan): The pool manager class is responsible for controlling access to the pooled objects. For example, ManBase is an abstract class that provides abstract methods for managing the pool, such as baseAdd, baseRemove, baseFind, etc. SpriteGameMan is a class derived from ManBase, which will specifically handle sprite objects.
   
2. Poolable Objects (SpriteGame and DLink): These are the objects stored in the pool. The NodeBase class serves as an abstract base for all objects that can be managed in the pool, whereas DLink is a class that would be used in a pool, inheriting from NodeBase.

3. Iterator (DLinkIterator): An iterator pattern is used with object pools for it to traverse through the objects in the pool.

### This object pooling architecture typically involves maintaining two lists:
1. Reserve List: A list of pre-loaded, inactive objects that are ready to be used.
2. Active List: The list of currently active objects that are in use within the game.
In practical terms, when managers like SpriteGameMan  need to create or add an object, they will check for availability in the reserve list. If the reserve list is empty, the manager creates new objects as specified by the reserveGrow. Once new objects are created or an existing object is called, it is moved to the active list. The transition between these lists is done by the ListBase class, which is pointed to by both the active and reserve lists. An iterator associated with these lists allows for efficient traversal through the objects.




# 2. ITERATING OF NODES (ITERATOR PATTERN) 
![image](https://github.com/user-attachments/assets/2167181c-8f21-48d8-baaf-927ce27a32d0)

Here, is the UML diagram of iterator pattern that I have used. 
Iterator pattern is useful for iterating through different type of data structures. 

In the game, images and textures are static assets loaded at startup, so they're stored in a singly linked list (SLink), which is simple and efficient for fixed data. Sprites, which can be added or removed during gameplay, are stored in a doubly linked list (DLink) to allow flexible updates.

However, using different structures means separate iteration logic, which breaks the uniform handling of game objects.

To maintain the homogeneous treatment of these objects while respecting their unique storage and management needs, using the Iterator Pattern offers a good solution. It provides a common interface to traverse both SLink and DLink, hiding structural differences. An abstract Iterator class defines this interface, and concrete classes like **SLinkIterator** and **DLinkIterator** implement the traversal logic. This allows the game to treat all asset types uniformly, regardless of how they're stored.


Iterator Pattern consists of two main key components:
1. Iterator Interface (Iterator): This class is either an interface of an abstract class, all classes derived from this class must define these methods.
2. Iterators: These are the classes which implement the methods from the interface or the abstract classes. These method implementations would vary from data structure to data structure.
   
Now the abstract methods are First(), Current(), IsDone(), Next():

1. First(): This will return the first element in the data structure and also reset the traversal.
2. Current(): This will return the current element where the traversal is at.
3. IsDone(): This will return a Boolean value that is the traversal is finished or not.
4. Next(): This will iterate to the next element of the data structure.

# 3. SPRITE PROXIES (PROXY PATTERN) 
![image](https://github.com/user-attachments/assets/07793a3e-c023-46de-b8a2-1291474f60aa)

Problem: For Space Invaders,The SpriteGame class holds a lot of data (e.g., position, scale, name, angle, image), but only position (x, y) is frequently updated for movement. Continuously managing this data can lead to performance inefficiencies.

The Proxy pattern provides a solution to this problem by creating a substitute for the SpriteGame class, by focusing only on the essential data such as position X and position Y.
We need to create SpriteGameProxy class which points to the real SpriteGame class.

Proxy pattern is a structural design pattern which creates an intermediate or middle object which also controls the access to the object and also what data can be passed to the real object.

Proxy pattern creates a light weight class that points to a class with real game sprite with more data.

Proxy pattern consists of three components:
1. **Subject Interface (SpriteBase):** This is the common interface or the class from which both RealSubject and Proxy are derived, ensuring that the Proxy can be used anywhere where is Real Subject is expected.
2. **RealSubject (SpriteGame):** The actual object that will perform the real operation. This contains the extensive data such as game sprite, and position, scale, name, angle, image, etc.
3. **Proxy (SpriteGameProxy):** The Proxy maintains a reference to the RealSubject and can call all the methods to the RealSubject. For performance optimization, the Proxy can handle the operations which are less resource intensive such as position X and position Y and pass the values to the RealSubject.

# 4. GAMEOBJECT FACTORIES (FACTORY PATTERN) 

**Challenge:** Creation of similar Game Objects with different types

**Problem:** So in Space Invaders, There are three different types of aliens Squid, Crab and Octopus. These game objects differ not only in types but also in their sprites, colors, and sizes.

**Solution:** Using the Factory Pattern is a strategic solution to address this complexity by encapsulating the object creation process, and also making the game architecture more manageable.

This factory abstracts away the details of the creation process from the code, and ease the game extension like adding new type of aliens and maintenance.

Here, is a basic code of how a factory creates an object:
![image](https://github.com/user-attachments/assets/7059c62a-56db-435e-86fe-79cd476bf36c)

**Pattern Description:**
This pattern is a creational design pattern and its primary objective is to offer a framework that abstracts the process of creation of objects and it can change the functionalities based on the specification passed.
Factory pattern consists of three main components:
1. Abstract products - this is the alien category that this object should be an alien.
2. Concrete products - these are the Squid, Crab, Octopus which are derived from Alien Category and each has its own unique sprites, colors and sizes. 
3. Creator - this is the AlienFactory which return an Gameobject which is a type of an alien. AlienFactory abstracts the creation logic, and encapsulates the details of instantiating each type of alien.

# 5. HANDLING TIME EVENTS (COMMAND PATTERN) 
Challenge: execute a certain functionality after a time is passed
Problem: From animating objects, movement and sound should occur after a certain time is passed. A certain functionality should be executed.
Solution: The command pattern provides a strategic and efficient solution to this problem where we can encapsulate a function as an object. 

COMMAND provides an interface that all objects derived from it must have that functionality.
When a certain timer frame is passed that functionality is called in all the command objects.
Command pattern is useful for delayed execution of a method.

![image](https://github.com/user-attachments/assets/55006d78-553d-4f95-817f-032025079cac)

Here, is the UML diagram of an example of using command pattern by integrating commands with timer events.

Pattern Description:
The Command Pattern is a behavioural design pattern that turns a request or functionality into an object containing all the information about the request. This will allow delaying or controlling a request’s execution. This is useful for operations which require a delayed
execution, such as animations, movement, sound and other events that need to occur after a certain time has passed.

There are 5 main components of Command Pattern:
1. **Command Interface (Command Class):** This is an interface or in our case an abstract class with an abstract method that executes the command. All the concrete command classes must implement this interface.
2. **Concrete Commands:** These are the specific implementations of the command interface. Each concrete command is responsible for particular action. In these commands we define the method to execute. For eg, SpriteAnimationCmd, MovementCmd, etc.

3. **Invoker (TimerEvent):** This is the class which will invoke the command. The invoker holds a command and at a point it ask a command to execute a request. The invoker doesn’t know the concrete commands and what is being performed.
4. **Client:** The client will connect the command object with a receiver and an action to perform.
5. **Receiver:** The receiver is the object that knows how to perform an operation.

For movement, sound and sprite animation all these must happen at certain timeframe. For moving the aliens at a certain time frame. MovementCmd will be executed when that time frame is passed. For example, I want to move the aliens at every 0.7 seconds. Then movement command will contain a data to move the aliens which will be executed when that time is passed. We are readding the timer event again at 0.7 seconds so the request in movement command will be executed every 0.7 second.
TimerEvent class holds these commands and these timer events are managed by a TimerEventMan class which will execute a request when a certain time frame is passed.

# 6. HIERARCHY BETWEEN GAME OBJECTS (COMPOSITE PATTERN) 
**Challenge:** Hierarchy of different game objects

**Problem:** Managing a hierarchy of game objects such as aliens, comprising of squid, crab and octopus and to handle individual aliens and groups of aliens (columns and grid) uniformly.
To handle operations such as movement, collision detection which are needed to be applied consistently across single aliens and groups without making codebase repetitive and with complex conditional statements.

**Solution:** The Composite Pattern solves this problem by treating both individual aliens (squid, crab, octopus) and their compositions (columns and grid) through a common interface or a class.
This will allow operations to be applied uniformly, whether it’s a single alien or a complex group.
![image](https://github.com/user-attachments/assets/53d18702-75c5-46d7-b2c0-7c1ee4122fa2)

Here, is the UML Diagram where I have used Composite Pattern for aliens.

**Pattern Description:**
The Composite Pattern is a structural design pattern that provides a way to compose objects into tree structures and then treat them as individual objects. This pattern is useful for creating hierarchy of objects where individual objects (leaf nodes) can be treated uniformly with the composition of objects (Composite Nodes).

The Composite Pattern consists of three main components:

1. **Component:** This is an interface or like in our case an abstract class defining all the common operations for both simple and composite objects. It will ensure that all objects are treated equally.
2. **Leaf:** A leaf has no children, each having their own specific behaviours. For eg, Squid, Crab, Octopus.
3. **Composite:** It is an object that has child components which can be either other composites or it can be leaf objects. Composites will implement the component interface and also define the behaviours for the components having children (Composites). For example, alien columns and alien grid are composites, where a grid can contain multiple columns, and each column can contain multiple aliens.

There are three types of aliens Squid, Crab and Octopus and these are single aliens which are leaf objects. Alien columns and alien grid are composite objects which consists of these aliens. An alien grid contains multiple alien columns and a column contains multiple aliens. Using this pattern, we treated all these objects uniformly for various purposes such as movement, collision, etc.


