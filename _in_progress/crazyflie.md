---
title: "Drone Swarm Light Painting"
author_profile: true
key: 0
excerpt: "Path planning, Swarm, ROS2, Drones"
header:
  teaser: /assets/images/crazyflie/crazyflie.jpeg
sidebar:
  - title: "Table of Contents"
  # - section: "Video Demo"
  #   url: /portfolio/crazyflie/#video-demo
  - section: "System Overview"
    url: /portfolio/crazyflie/#system-overview
  - section: "Hardware"
    url: /portfolio/crazyflie/#hardware
  # - section: "Handle Detection"
  #   url: /portfolio/crazyflie/#handle-detection
  # - section: "Pouring"
  #   url: /portfolio/crazyflie/#pouring
---

# This project is currently in progress
This project uses three Crazyflie Drones to create a long-exposure picture. The camera captures the light emitted by the on-board LEDs over the course of the drones trajectory to create images. 

Source code: [GitHub](https://github.com/kylew239/light-painting-swarm)

<!-- ## Video Demo -->


## System Overview
![Block Diagram]({{ site.url }}{{ site.baseurl }}/assets/images/crazyflie/SystemDiagram.png)

This project utilizes mutliple ROS nodes interfacing with the various hardware and the Crazyflie server ([Crazyswarm2 Package](https://imrclab.github.io/crazyswarm2/)). I created various nodes based on the difference functionalities needed, such as camera control, trajectory generation, and drone control.


## Hardware
The following hardware was used in this project:
* Crazyflie 2.1
* CrazyRadio 2.0
* Lighthouse positioning system
* Sony A6400 DSLR Camera
* Arduino Uno