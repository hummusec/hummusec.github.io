---
title: 'Crash Course: Your first Flipper Zero app'
date: 2023-06-18 18:00:00 +0200
categories: [Flipper Zero]
tags: [flipper_zero, development]
---

# Introduction

This tutorial will guide you through the process of creating your first Flipper Zero app. We will create a simple Hello World app that will be a good starting point for your future projects.

We will take a look at how to setup the development environment, how to create a new app, how to build it and how to deploy it to your Flipper Zero using a FAP (Flipper Application Package) file.

# Preparing the development environment

Before getting started with developing the we need to setup our development environment.

## Getting the Flipper Zero firmware

First, we need to get a copy of the [Flipper Zero firmware repository](https://github.com/flipperdevices/flipperzero-firmware).

>We are getting the official firmware regardless of whatever custom firmware you are currently using.
{: .prompt-tip }

Make sure you have enough disk space (about 2GB) and clone the source code:
```bash
git clone --recursive https://github.com/flipperdevices/flipperzero-firmware.git
```

Building

Build firmware using Flipper Build Tool:

./fbt
