---
title: "EKF SLAM"
author_profile: true
key: 0
excerpt: "Extended Kalman Filter, Localization, C++"

# Makes this hidden on the main site, and redirects to the main
hidden: true
redirect_to: /portfolio/slam

header:
  teaser: /assets/images/slam/turtlebot.jpeg
sidebar:
  - title: "Table of Contents"
  - section: "Video Demo"
    url: /portfolio/slam/#video-demo---ekf-slam-in-simulation
  - section: "Kinematics"
    url: /portfolio/slam/#kinematics
  - section: "Simulation"
    url: /portfolio/slam/#simulation
  - section: "Robot Control"
    url: /portfolio/slam/#robot-control
  - section: "Extended Kalman Filter SLAM"
    url: /portfolio/slam/#extended-kalman-filter-slam
  - section: "Performance In Simulation"
    url: /portfolio/slam/#performance-in-simulation

---
<!-- This project involves building an Extended Kalman Filter Simultaneous Localization and Mapping (EKF-SLAM) Algorithm from scratch. This algorithm was then implemented on a TurtleBot3 and tested with cylindrical obstacles. This project was completed using ROS2 Iron and C++.

Source code: [GitHub](https://github.com/kylew239/EKF-SLAM)\
Project Timeframe: 1/03/24 - 3/16/24

## Video Demo - EKF-SLAM in Simulation
<iframe width="560" height="315" src="https://www.youtube.com/embed/NvknFuvAxmg?si=F2ZKNfARoSRp7CFR" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


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


## Extended Kalman Filter SLAM
This feature is currently a work in progress.

The SLAM pipeline for this project involves two main inputs: wheel encoders and a 2D LiDAR. The SLAM algorithm calculates the odometry of the robot using features detected by the LiDAR.


## Performance In Simulation
Ground Truth:
```
x: 0.0 m
y: 0.024 m
θ: -168.070 deg
```

Odometry:
```
x: -0.278 m
y: -0.057 m
θ: -168.070 deg
```

EKF-SLAM:
```
x: -0.001
y: 0.024
θ: -168.05 deg
```

Odomotery data had a positional error of 0.289m and no rotational error. Given that collisions were programmed with no rotational component, this data makes sense. The odometry data, with no sensor noise and no rotational collisions, is off linearly but is perfect in terms of the angular position

EKF-SLAM data had a positional error of 0.001 m and a rotational error of 0.02 deg. This data is calculated from both LiDAR and odometry data, so it should be relatively accurate. As expected, EKF-SLAM greatly outperforms odometry data, especially when collisions are involved. -->