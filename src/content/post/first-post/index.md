---
title: "def __init__(self)"
description: "If only something were as easy as python, but sadly they aren't. getting my hands wet with opengl"
publishDate: "12 Nov 2023"
tags: ["tech"]
---

## motivation
ever since I have been programming, the primary motivation I have always had is to build cool stuff. i have always treated it like a hobby, which is why i tinker around with it so much. for the past few weeks i was looking to work on something new, something that is exciting and challenging enough at the same time. essentially i wanted to build something that i could be proud of. just then i ran into this [video](https://www.youtube.com/watch?v=lMvFWKHhVZ0). unlike other tech content,it provided me a different perspective on approaching things. it gave me the motivation to go beneath the layers of abstraction. hence i decided to make my own game engine. idk if i will ever be able to finish it, but the very thought sounded exciting to me.


## initial steps
so to make a game engine, you would need to render graphics on your screen. now the best way to do that was to use OpenGL, and this is the purpose of this blog. i would teach you how to setup your OpenGL environemnt, especially on mac. we would be setting up the _GLFW_ and _GLAD_ for this. it took me so much time to figure this out, since there isn't a dedicated blog that helps you setup both these things end to end. so here it is.

## a little background 

before moving forward with the setup, let me give you a few definitions of what exactly each thing is and what it does.
1. opengl: OpenGL is a cross-language, cross-platform application programming interface for rendering 2D and 3D vector graphics. The API is typically used to interact with a graphics processing unit, to achieve hardware-accelerated rendering. to be precise it isn't even an api, it is a specification. it depends on graphics card manufacturers to implement it. hence a lot of these libraries are written and maintained by them.
2. glfw: GLFW is an Open Source, multi-platform library for OpenGL, OpenGL ES and Vulkan development on the desktop. It provides a simple API for creating windows, contexts and surfaces, receiving input and events. 
   1. context is the complete state of the opengl instance. it stores all the data and buffers that are required to render the graphics.
3. glad: Glad is an open source library that manages the loading of OpenGL functions. It provides a simple API for creating windows, contexts and surfaces, receiving input and events.

## detailed steps
the steps I am providing are very specific to mac. if you are on windows or linux, you can follow however i would recommend you to just google steps for your os, since there are many resources available for that. 

we would be using c++ (language for real developers) for this. so make sure you have some installed clang on your system. apart from this we would be using visual studio code for this tutorial, however the tutorial is IDE agnostic. so you can use any IDE you want.

### setup glfw:
   There are multiple approaches you can take here. you can either install it using homebrew or you can download the binaries availabe on the official website. however i tried both these approaches and i didn't find any success in them. so i would recommend you to download the source code and build it yourself.
   1. clone the source code from [here](https://github.com/juliettef/GLFW-CMake-starter) 
   ``` bash
    git clone --recursive https://github.com/juliettef/GLFW-CMake-starter
   ```
   2. download cmake on your system. 
   3. enter the directory _GLFW-CMake-starter_ and run the following commands
   ``` bash
    mkdir build
    cd build
    cmake ..
    make
    sudo make install
   ```
   now if you check the folder _/usr/local/include_ you would find a folder named _GLFW_. this means that glfw has been successfully installed on your system. apart from this you can also find the binaries in _/usr/local/lib_. eventually your folder structure will look something like this 
   ``` bash
   ├── include
   │ └── GLFW
   │    ├── glfw3.h
   │    └── glfw3native.h
   └── lib
      ├── cmake
      │ └── glfw3
      │ ├── glfw3Config.cmake
      │ ├── glfw3ConfigVersion.cmake
      │ ├── glfw3Targets-noconfig.cmake
      │ └── glfw3Targets.cmake
      ├── libglfw3.a
      └── pkgconfig
      └── glfw3.pc
   ```
   now if you should be able to use the glfw header files in your code. to test this create a file named _test.cpp_ and add the following code to it.
   ``` cpp
   #include <GLFW/glfw3.h>
   #include <iostream>
   ```
   if the above code doesn't throw any error, then you have successfully installed glfw on your system. You should also receive intellsense in your IDE.

### setup glad:
now the next step is to setup glad. for this visit their official website [here](https://glad.dav1d.de/). make sure you select the following options
1. language: c/c++
2. specification: opengl
3. profile: core
4. api: gl version 4.1

now press generate and download the zip file. extract the zip file and you would find two folders named _include_ and _src_. copy the contents of _include_ folder to _/usr/local/include_ 
``` bash
cp -r include/* /usr/local/include
```
now you shall be receiving intellsense for glad as well.

### final step: configure the makefile
now the final step is to create a Makefile to compiler our code. create a folder named _myCoolProject_. create a sub-directory named _src_ and add a file named _main.cpp_ to it. now add the _Makefile_ to the root directory. the contents of the Makefile should be as follows
``` makefile   
APP_NAME = build
BUILD_DIR = ./bin
C_FILES = ./src/*.cpp
GLAD_FILE = ./src/glad.c

APP_DEFINES :=
APP_INCLUDES:= -I/usr/local/include -framework Cocoa -framework OpenGL -framework IOKit
APP_LINKERS:= -L/usr/local/lib/ -lglfw3 -v

build:
	clang++ $(C_FILES) $(GLAD_FILE) -o $(BUILD_DIR)/$(APP_NAME) $(APP_INCLUDES) $(APP_LINKERS)%                                                           
```
now run the following command to compile your code
``` bash 
make build
```
if you see a binary in the bin folder then you have successfully setup your opengl environment. now you can start building all the cool stuff using this. 

## conclusion
so this week i managed to get my environment up and running. tbh this took hours and hours of debugging, since i haven't built enough projects using c++ before. now i am planning to go deeper into sharders, lighting, textures and all that jazz. i would be following these two resources over the week
1. https://learnopengl.com/Introduction
2. https://play.google.com/books/reader?id=qFstEAAAQBAJ&pg=GBS.PA83&hl=en_IN 

most probably i would build some sort of simple visualtion tool by the next weekend so stay tuned for that 

