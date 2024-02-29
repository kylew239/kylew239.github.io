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
  - section: "Simulation"
    url: /portfolio/slam/#simulation
  - section: "Robot Control"
    url: /portfolio/slam/#robot-control
  # - section: "Simulation"
  #   url: /portfolio/slam/#simulation

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
A custom simulation environment was designed by using RVIZ. This is handled via a ROS2 Node that simulates robot position and obstacles. The red figure represents the "real" position of the robot. This node simulates the following:
* Robot position (with noise and slippage)
* Lidar sensor data (with noise)
* Obstacle collisions

![simulation]({{ site.url }}{{ site.baseurl }}/assets/images/slam/nusim.png)

## Robot Control
The robot is controlled by converting incoming `Twist` messages to wheel commands which directly control the robot wheels. This is done using the custom kinematics library. The odometry of the robot is calculated using the published `JointState` messages along with the same kinematics library. The odometry of the robot can be visualized in the simulation environment - it is represented by the blue figure. 

In the simulation, with perfect odometry, the blue figure lines up with the red figure, since the odometry would perfectly calculate the position of the robot. When there is noise, wheel slippage, or collisions, the blue figure would not line up with the actual position.

<!-- TODO: Insert image after collision to show that red and blue don't line up. -->