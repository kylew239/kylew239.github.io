---
title: "Robotic Coffee Maker"
author_profile: true
key: 4
excerpt: "Trajectory planning, Object manipulation, ROS2, Moveit, OpenCV"
header:
  teaser: /assets/gifs/botrista.gif
---
This project uses the Franka Emika Panda arm to brew a cup of pour over coffee. It uses computer vision and AprilTags to detect where each object is and how to grasp the object, and it uses Moveit2 to plan the trajectories.

Source code: [GitHub](https://github.com/kylew239/Botrista-Robotic-Coffee-Maker)\
Moveit2 Wrapper: [GitHub](https://github.com/kylew239/Moveit2-Wrapper)\
Group Members: Stephen Ferro, Carter DiOrio, Anuj Natraj, Kyle Wang, Jihai Zhao

## Video Demo
<iframe width="897" height="505" src="https://www.youtube.com/embed/INRJ8Y_SD4U" title="Making Coffee with a Robot Arm: Botrista" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


## Moveit Wrapper
This project uses a custom wrapper for the Moveit2 API. The purpose of this wrapper is to make implentation easier - it automatically fills in many of the message fields, and offers a simpler way of planning trajectories. Some of the notable features of this wrapper are:

- A grasp planner
  - Offers an easy way to set the expected payload
  - Moves to an approach pose, then a grasp pose, closes the gripper, and moves to a retreat pose
- Plan
  - Calculates inverse kinematics to move the end-effector of the robot to a given position and/or orientation
- Cartesian Trajectory
  - Plans a trajectory to move the end-effector through a series of poses
- Trajectory Constraints
  - Create position/orientation constraints for the end-effector
  - Maintain end-effector orientation while planning and executing a trajectory


## AprilTags
AprilTags were used for localization. A camera was mounted on the ceiling so that it could see all of the AprilTags. The following were used:

- One large AprilTag on the table
  - This was used to localize the camera
- One AprilTag for each graspable object
  - These were placed on acrylic plates that the objects were mounted/attached to
  - These allowed the robot to see the general location of each object

![April Tags]({{ site.url }}{{ site.baseurl }}/assets/images//botrista/aprilTags.jpg)


## Handle Detection
When picking up an object, the robot arm will first move above the AprilTag associated with that object. At that point, the camera mounted onto the arm will search for the handle. This was done by attaching blue and green tape to the handle, and using computer vision to find the handle and the orientation needed.\
![Handle]({{ site.url }}{{ site.baseurl }}/assets/images//botrista/handle.png)

The image below depicts what the camera sees. The blue tape is found using a color mask, and the centroid of it is drawn in the image. The green tape is found using another color mask. Once these two colors are detected, a line is drawn from the centroid of the blue tape to the centroid of the green tape.\
![rviz]({{ site.url }}{{ site.baseurl }}/assets/images//botrista/rviz.png)