---
title: "Drone Swarm Light Painting"
author_profile: true
key: 6
excerpt: "Path planning, Swarm, ROS2, Drones"
header:
  teaser: /assets/gifs/crazyflie.gif
sidebar:
  - title: "Table of Contents"
  - section: "Video Demo"
    url: /portfolio/crazyflie/#video-demo
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
  - section: "Flight Path Verification"
    url: /portfolio/crazyflie/#flight-path-verification
  - section: "Light Painting with Multiple Drones"
    url: /portfolio/crazyflie/#light-painting-with-multiple-drones
---
This project uses three Crazyflie Drones to create a long-exposure picture. The camera captures the light emitted by the on-board LEDs over the course of the drones trajectory to create images. 

Source code: [GitHub](https://github.com/kylew239/light-painting-swarm)\
Project Timeframe: 1/03/24 - 3/16/24

## Video Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/ww7sDnqF3a0?si=ehcX_rwx6OKvxZt9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## System Overview
![Block Diagram]({{ site.url }}{{ site.baseurl }}/assets/images/crazyflie/SystemDiagram.png)

This project interfaces multiple ROS nodes with the Crazyflies, camera, and Crazyflie Server. ([Crazyswarm2 Package](https://imrclab.github.io/crazyswarm2/)). These nodes were responsible for shutter control, trajectory generation, and drone control.


## Hardware
The following hardware was used in this project:
* Crazyflie 2.1: The drone
* CrazyRadio 2.0: Radio responsible for communication with the drones
* Lighthouse positioning system: Optical positioning system with sub-millimeter precision
* Sony A6400: DSLR Camera for Long Exposure Photography
* Arduino Uno: Controls the DSLR Camera

## Camera Control
The Sony A6400 DSLR Camera has the Sony Multi-purpose Interface port. This port allows us to control the camera. By using a 2.5mm to Multi-purpose Interface adapter, we can control the camera's shutter by shorting the tip, ring, and sleeve of the 2.5mm cable. The connections are shown in the schematic below. Pulling the Arduino pin low starts the shutter, while pulling the pin high releases the shutter. This camera supports bulb exposure mode, so the long-exposure shot length can be controlled to match the flight time.

![Schematic]({{ site.url }}{{ site.baseurl }}/assets/images/crazyflie/camera_schematic.png)


## Waypoint Generation
To control the flight path of the drones, I decided to use waypoints that the drone could follow. This was accomplished through the following steps:
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


## Flight Path Verification
In order to ensure that the drone was flying the correct path, I used OpenCV to help trace the path of the drone in `light_painting/script/visualize.py` This script was used in both demo videos to help visualize the paths flown.

This diagram shows the logic flow of this script.

![visualize]({{ site.url }}{{ site.baseurl }}/assets/images/crazyflie/visualize.png)

## Light Painting with Multiple Drones
I modified the ROS2 nodes so that multiple drones can be added by just changing the launch file and the `config.yaml` file. For the video demo at the top of this page, the following changes were made:
* The URI's of the additional drones were added to the `light_painting/config/config.yaml` file
* I created the `light_painting/launc/light_paint_three.launch.py` file by duplicating the `flight` and `led` nodes multiple times, with different names and colors for each drone
