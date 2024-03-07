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
  - section: "Camera Control"
    url: /portfolio/crazyflie/#camera-control
  - section: "Waypoint Generation"
    url: /portfolio/crazyflie/#waypoint-generation
  - section: "Light Painting with One Drone"
    url: /portfolio/crazyflie/#light-painting-with-one-drone
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

## Camera Control
The Sony A6400 DSLR Camera has the Sony Multi-purpose Interface port. This port allows us to control the camera. By using a 2.5mm to Multi-purpose Interface adapter, we can control the camera's shutter by shorting the tip, ring, and sleeve of the 2.5mm cable. The connections are shown in the schematic below. Pulling the Arduino pin low starts the shutter, while pulling the pin high releases the shutter. This camera supports bulb exposure mode, so the long-exposure shot length can be controlled to match the flight time
![Schematic]({{ site.url }}{{ site.baseurl }}/assets/images/crazyflie/camera_schematic.png)


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


## Light Painting with One Drone
The drone is commanded to navigate through the generated waypoints. In order for the final image to resemble the input image, the onboard LEDs are controlled in one of two ways:
* The LED is turned on when the drone's position is within a threshold radius of the waypoint
* The LED is turned on when the drone's position lies on the line formed by the previous waypoint and the next waypoint

This video demo uses the same tree example from earlier, with the LED controller using the first method and a radius of 3cm.
<iframe width="560" height="315" src="https://www.youtube.com/embed/ruHbgud3S4g?si=n_Qlzbt_qk-Qytv6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>