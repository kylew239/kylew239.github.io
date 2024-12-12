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
    url: /portfolio/shepherd/#shepherding-and-diffusion-policy
  - section: "Pygame Simulation"
    url: /portfolio/shepherd/#pygame-simulation
  - section: "Inputs and Observations"
    url: /portfolio/shepherd/#inputs-and-observations
  - section: "Training Analysis"
    url: /portfolio/shepherd/#training-analysis
  - section: "Limitations and Future Work"
    url: /portfolio/shepherd/#limitations-and-future-work
  - section: "References"
    url: /portfolio/shepherd/#references
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

This picture displays 24 shepherding trials. Each trial has the same initial goal and sheep positions, with slightly varying shepherd positions. A diffusion policy model trained on this image  would attempt to herd the sheep by following the red path. However, the model would fail to herd sheep with different initial positions, since there is no data for that. To create a generalized model, I would also need to use data with varying initial sheep positions.


## Pygame Simulation
In order to collect data to train the model, and to evaluate the model, I needed a simulation environment. I decided to use PyGame since it satisfies following requirements:
- Easy to modify
- Allows user input (keyboard or controller)
- Can save the data (Using CSV files and images)
- Has easily tunable parameters
- Can display the game state visually

I used the [Strombom Model](https://royalsocietypublishing.org/doi/10.1098/rsif.2014.0719){:target="_blank"} to control the sheep. Most of the parameters are the same as the ones described in the paper, but I changed some to make herding easier. The resulting pygame window is shown below. The game uses extremely simply graphics, with each object represented by a circle. The sheep and shepherd have their headings represented by a triangle.
![pygame]({{ site.url }}{{ site.baseurl }}/assets/images/shepherd/pygame.png)

The state at each instance of the game is saved. The image is saved as a `.bmp` file while the positions are saved in a csv, in the following format:
```
data                    # Contains data for each game run
└── 1  
    └── img             # Contains the image at each frame, as a bmp
        └── 0.bmp
        └── 1.bmp
        └── ...
    └── pos.csv         # Contains the shepherd positions per frame
    └── sheep_pos.csv   # Contains the sheep positions per frame
    └── target_pos.csv  # Contains the target position
└── 2  
└── ...
```


## Inputs and Observations
Part of the project was figuring out what inputs and observations are a good choice. From the pygame simulation, positions and images are directly obtainable. Other variables can also be calculated, such as center of mass of the sheep or distance to the goal. 

Using images as an observation also makes the model significantly worse. The GIF below shows 8 evaluations - the top row is a model trained with images, and the bottom row is a model trained without images. Apart from image data, both models were trained on the same set of data, with the same amount of information. The light blue path is the path that the shepherd has taken so far.
![img_low]({{ site.url }}{{ site.baseurl }}/assets/gifs/shepherd_image_vs_low.gif)

This behavior makes sense - the image is extremely noisy from a computer vision perspective, since the image data just has a single pixel changing and moving. Diffusion Policy uses a CNN for training using image data, which is great for picking up patterns in images. However, the image data from the PyGame simulation only has a single pixel moving around - which isn't enough for the model to learn from. As a result, the image model failed to herd the sheep to the goal in most evaluations.

Adding other information, especially information dependent on other variables, also seemed to negatively affect the model performance. This is because this data doesn't provide any new information, and acts as noise during the training process. The best model obtained was trained using just the positions of the sheep and shepherd.


## Training Analysis

## Limitations and Future Work

## References
[Diffusion Policy Paper](https://arxiv.org/abs/2303.04137){:target="_blank"}\
[Strombom Model](https://royalsocietypublishing.org/doi/10.1098/rsif.2014.0719){:target="_blank"}\
[Nick Morales Diffusion Policy repository](https://github.com/ngmor/diffusion_policy/tree/main){:target="_blank"}

Thanks to Matt Elwin, Lin Liu, Abhishek Sankar, Ishani Narwankar, and Courtney Smith for guidance and collaboration in this project