---
title: "EKF SLAM"
author_profile: true
key: 0
excerpt: "Extended Kalman Filter, Localization, C++"
header:
  teaser: /assets/images/slam/turtlebot.jpeg
sidebar:
  - title: "Table of Contents"
  # - section: "Video Demo"
  #   url: /portfolio/botrista/#video-demo
  - section: "Kinematics"
    url: /portfolio/slam/#kinematics
  - section: "Simultion"
    url: /portfolio/slam/#simulation

---

# This project is currently in progress
This project involves building an Extended Kalman Filter Simultaneous Localization and Mapping (EKF-SLAM) Algorithm from scratch. This algorithm was then implemented on a Turtlebot3 and tested with cylindrical obstacles

Source code: [GitHub](https://github.com/kylew239/EKF-SLAM)

<!-- ## Video Demo -->


## Kinematics
The kinematics library for this projected was developed in C++, and handles calculations involving the kinematics and transformations of the robot. This library can be found under the turtlelib folder in the code. This library contains the following files:
- geometry2d - Handles 2D geometry primitives such as vectors and points.
- se2d - Handles 2D rigid body transformations
- svg - Creates SVG drawings from points, vectors, and coordinate frames

## Simulation
A custom simulation environment was designed by using RVIZ. This is handled via a ROS2 Node that simulates robot position and obstacles.

![simulation]({{ site.url }}{{ site.baseurl }}/assets/images/slam/nusim.png)
