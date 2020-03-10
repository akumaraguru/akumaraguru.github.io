---
layout: page
title: Kickstarting Meta-RL with Expert Demonstrations
permalink: /projects/kickstart-metarl/
---

{% include image-caption.html
    url="/assets/images/rlkickstart_schematic2.png"
    description="Schematic of data flow. We initialize our experience buffer with expert demonstrations to speed up exploration."
%}

Inspired by [Hausman et al. 2018](https://openreview.net/forum?id=rk07ZXZRb) and [Julian et al. 2018](https://ryanjulian.me/iser_2018.pdf), which explored how an embedding space of trajectories can be exploited to reuse and interpolate task-specific knowledge in a multitask setting, this group project sought to optimize this framework by adding two components:

1) Initialize the embedding with expert demonstrations for each task to be learned to speed up exploration during training.

2) Shape the trajectory embedding with a Variational Autoencoder to provide a dense prior that can be more useful for interpolation.

I developed an imitation learning algorithm in Tensorflow using the [Garage](https://github.com/rlworkgroup/garage) toolkit, and built new multitask environments and expert datasets for testing.

[project report](https://drive.google.com/open?id=1ftPdQn2WfZjwarwWqYPfnn0iVnVyf_px)

{% include image-caption.html
    url="/assets/images/rlkickstart_toyenv.png"
    description="Simulation of multitask environment in MuJoCo. A Sawyer arm uses a graspable peg (in blue) to manipulate a box with a lid."
%}