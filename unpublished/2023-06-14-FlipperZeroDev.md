---
title: 'Crash Course: Your first Flipper Zero app'
date: 2023-06-18 18:00:00 +0200
categories: [Flipper Zero]
tags: [flipper_zero, development]
---

# Introduction

This tutorial will guide you through the process of creating your first Flipper Zero app. We will create a simple Hello World app with a Scene Manager that will be a good starting point for your future projects on the Flipper Zero.

We will take a look at how to setup the development environment, how to create a new app package from scratch, and how to build & deploy it to your Flipper Zero device.

# Preparing the development environment

Before getting started with developing the we need to setup our development environment.
If you already have a working development environment, and know how to use `./fbt`, you can safely skip this section and jump straight to [Creating a new Flipper Application Package](#creating-a-new-flipper-application-package).

## Getting the Flipper Zero firmware

First, we need to get a copy of the [Flipper Zero firmware repository](https://github.com/flipperdevices/flipperzero-firmware).

>We are getting the official firmware regardless of whatever custom firmware you are currently using. As long as the API levels match, we can use the official firmware to develop apps for any custom firmware.
{: .prompt-tip }

Make sure you have enough disk space (about 2GB) and clone the source code:
```bash
git clone --recursive https://github.com/flipperdevices/flipperzero-firmware.git
```

Next, we will run `./fbt` once, it will download the toolchain and will build the firmware for the first time.
```bash
cd flipperzero-firmware
./fbt
```

## Installing Visual Studio Code environment
After the process has completed, we will run `./fbt` again to deploy the Visual Studio Code environment to our `flipperzero-firmware` directory.
```bash
./fbt vscode_dist
```

Now we can open the `flipperzero-firmware` directory in Visual Studio Code and start developing our app.

# Creating a new Flipper Application Package

Now that we have our development environment setup, we can preparing our files for creating our first Flipper Application Package (FAP).

All user applications are stored in the `applications_user` directory of the `flipperzero-firmware` directory.

We will create a new sub-directory for our app, name it `hello_world`.

## Creating the `application.fam` file

Inside the new directory, create a new file called `application.fam`. 

This small python code snippet, forming a call to the App() function with various parameters, will contain the metadata for our app.

```python
App(
    appid="hello_world",              # Mandatory, must be unique
    name="Hello World",               # App name
    apptype=FlipperAppType.EXTERNAL,  # App type (EXTERNAL, SYSTEM, etc.)
    entry_point="hello_world_app",    # Entry point function name
    cdefines=["APP_HELLO_WORLD"],     # C defines
    requires=[                        # List of required modules
        "gui",
        "storage",
        "notification",
        "dialogs",
    ],
    provides=[],                      # List of provided modules
    stack_size=2 * 1024,              # Stack size
    order=1,                          # Order in the menu
    fap_icon="icons/Hi_10x10.png",    # Icon file for the menu entry
    fap_category="Samples",           # Category in the menu
    fap_icon_assets="icons",          # Icon assets directory
    fap_version=(0, 1),               # Version: (major, minor)
    fap_description="Hello World",    # Description
)
```

There are more parameters available, you can read more about AppManifests in the [Flipper Zero documentation](https://github.com/flipperdevices/flipperzero-firmware/blob/dev/documentation/AppManifests.md#application-definition)

## Application Icon

We will also need to create an icon for our app. The icon will be displayed in the Flipper Zero menu.

It needs to be 10x10 pixels, 1-bit color depth, PNG format. Like this:

![Hi_10x10.png](/assets/img/attachments/2023-06-14-FlipperZeroDev.md/Hi_10x10.png)

# Scene Manager

A Scene Manager is a class that manages the scenes of your application. It is responsible for creating, navigating between, and destroying scenes.

Not only that it is easier to manage and navigate between scenes using a Scene Manager, but it also allows you to reuse a collection of components and you don't need to re-invent the wheel. These components include:

- Buttons
- Menus / Submenus
- File Input
- Text Inputs
- Loading screens
- Widget components (like text labels, scroll-box, frame, icon, etc.)
- And more...

There are some disadvantages to using a Scene Manager, it is overkill for simpler applications (use something called "View Port" instead), and it is not very well documented (like most of the Flipper Zero firmware).



## Scene Callbacks

For each one of our scenes, we will need to create 3 callback functions:




# View Dispatcher


First we will define an enum that will contain the names of all our scenes:
```c
typedef enum {
    AppSceneMenu,
    AppSceneHello,
    AppSceneWorld,
    AppSceneCount // This is not a scene, it is used to count the number of scenes
} appScene;
```

Then we will define an enum that will contain the names of all our views:
```c
typedef enum {
    AppViewKnob,
    AppViewWidget
} appViews;
```
















## Creating a Scene Manager

## File structure

So far you should have a directory structure like this:

```
applications_user/
└── hello_world/
    ├── application.fam
    └── icons/
        └── Hi_10x10.png
```








If followed the instructions correctly, you should now have a new directory structure like this:

```
applications_user/
└── hello_world/
    ├── icons/
    │   └── Hi_10x10.png
    └── scenes/
        └── 
    
```


# References / Additional Links

## Flipper Zero - Creating UI using Scenes

Video tutorial series by Derek Jamison on how to create UI using Scenes.
[Flipper Zero - Part 1 - Creating UI using Scenes](https://www.youtube.com/watch?v=YbskaB6caqk)