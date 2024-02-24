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
  - section: "Waypoint Generation"
    url: /portfolio/crazyflie/#waypoint-generation
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


## Waypoint Generation
To control the flight path of the drones, I decided to use waypoints that the drone could follow. This was accomplished through the following steps
1. Read the image
2. Apply Grayscale and Gaussian Blur
3. Use Canny Edge Detection with thresholds of 400 and 500
4. Use `numpy.nonzero` to get a list of pixels/points that the edges correspond to
5. Sort the list of points using a Nearest Neighbor algorithm to create a path that can be followed
6. Transform the points into the real-world coordinate frame.

This animation demonstrates the process of generating the waypoints
<iframe width="560" height="315" src="https://www.youtube.com/embed/XoIfsbLARS8?si=EVLhfCZlSi3q5GVE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>