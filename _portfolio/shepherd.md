---
title: "Shepherding Model From Human Behavior"
author_profile: false
key: 7

excerpt: "Machine Learning, Diffusion Policy, Pytorch, Demonstration Learning"
header:
  teaser: assets/gifs/shepherd.gif
sidebar:
  - title: "Table of Contents"
  - section: "Video Demo"
    url: /portfolio/shepherd/#video-demo
  - section: "Shepherding and Diffusion Policy"
    url: /portfolio/shepherd/#Shepherding-and-Diffusion-Policy
  - section: "Pygame Simulation"
    url: /portfolio/shepherd/#Pygame-Simulation
  - section: "Inputs and Observations"
    url: /portfolio/shepherd/#Inputs-and-Observations
  - section: "Training Analysis"
    url: /portfolio/shepherd/#Training-Analysis
  - section: "Limitations and Future Work"
    url: /portfolio/shepherd/#Limitations-and-Future-Work
  - section: "References"
    url: /portfolio/shepherd/#References
---
## This page is still in progress

This project is focused on machine learning and aims to build a shepherding model based on human behavior. A simulation and data collection environment was built using pygame. Data was collected before being put into the training and evaluation pipeline. This project implements an [Action Diffusion](https://arxiv.org/abs/2303.04137){:target="_blank"} machine learning model.

GitHub: [Shepherd Game](https://github.com/kylew239/Shepherd_game){:target="_blank"}\
GitHub: [Diffusion Policy](https://github.com/kylew239/diffusion_policy){:target="_blank"}

## Video Demo

## Shepherding and Diffusion Policy
Robotic shepherding involves using robots to guide a group of animals, such as livestock, towards a designated target. The challenge lies in coordinating multiple animals in a dynamic environment, where each animal's behavior can be unpredictable. While a traditional algorithmic approach can work, it can struggle with unpredictable behavior and random starting environments. However, for shepherding dogs (and humans, to some extent), this problem is easily solved with intuition. 

This is where diffusion policy comes into play. By sampling a distribution of human data, diffusion policy can generate actions and behaviors based off of human intuition. By manually herding sheep from different initial conditions, we can build a generalized shepherding model that mimics human intuition to successfully herd the sheep.

![24 paths]({{ site.url }}{{ site.baseurl }}/assets/images/shepherd/24.png)

This picture displays 24 shepherding trials. Each trial has the same initial goal and sheep positions, with slightly varying shepherd positions. A diffusion policy model trained on this image  would attempt to herd the sheep by following one of the paths.


## Pygame Simulation

## Inputs and Observations

## Training Analysis

## Limitations and Future Work

## References
[Diffusion Policy Paper](https://arxiv.org/abs/2303.04137){:target="_blank"}\
[Strombom Model](https://royalsocietypublishing.org/doi/10.1098/rsif.2014.0719){:target="_blank"}\
[Nick Morales Diffusion Policy repository](https://github.com/ngmor/diffusion_policy/tree/main)

Thanks to Matt Elwin, Lin Liu, Ishani Narwankar, Abhishek Sankar, and Courtney Smith for guidance and collaboration in this project