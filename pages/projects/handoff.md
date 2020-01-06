---
layout: page
title: Handoff Helper
permalink: /projects/handoff/
---

{% include youtubePlayer.html id="h2sRtbuoD5Q" %}

[source code](https://github.com/akumaraguru/ee106b/tree/master/project4)

This project was inspired by the [DexNet](https://berkeleyautomation.github.io/dex-net/) grasp database, which aimed to provide a pollable source of robust grasps for a parallel-gripper robot. With the assumption of a reliable, high-bandwidth connection to the internet, we developed a methodology to generate candidate grasps from object meshes using classical methods and subsequently choose optimal grasps for handoff operations (robot-to-robot or robot-to-human) in an efficient manner.

Our group, composed of myself, [Scout Heid](https://www.linkedin.com/in/scout-heid/), and [Wesley Guo](https://www.linkedin.com/in/wesley-yuan-guo/), developed this project (titled Handoff Helper - naming credits go to Wesley) as the final project for our class on robotic grasp analysis in Spring of 2016.

![Closeup of a grasp optimal for handoff](/assets/images/handoff-closeup.jpg){:class="img-responsive"}

The theoretical foundation for the grasp calculations was force closure analysis. This allows us to generalize the grasp and handoff operation using any finger or hand contact model. By looking at the friction cones and contact point position vectors, one can determine valid grasps under the force closure criterion. In our specific application we modeled the grasp as a soft-fingered two point contact using a parallel gripper

![Software Architecture](/assets/images/handoff-arch.png){:class="img-responsive"}

Our approach splits the required work into the computationally-heavy offline stage, and real-time online stage. 

The offline phase will build a library of valid grasps, and rank pairs of grasps that are most ideal for handoff operations. There are three main components: force closure pair generation, grasp generation, and grasp pair evaluation.The most computationally intensive part of this phase is embarrassingly parallelizable, allowing us to process a large quantity of objects quickly with large compute servers.

The online phase focuses on localizing the object within its work-space and computing the motion planning necessary to execute the grasp. We use AR markers to simplify the localization procedure.

![Software Visualization](/assets/images/handoff-rviz.png){:class="img-responsive"}
