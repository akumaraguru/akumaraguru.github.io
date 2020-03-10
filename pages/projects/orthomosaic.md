---
layout: page
title: Orthomosaicing for Aquatic Imagery
permalink: /projects/orthomosaic/
---

![Stitched image of the Aukerman dataset](/assets/images/orthomosaic-aukerman.png){:class="img-responsive"}

*This project is currently a work in progress! More information (including source code) will be provided once we have published.*

Collecting detailed imagery of a survey area often involves flying an aerial vehicle to take multiple pictures from a top-down perspective and then stitching them together in a process called orthomosaicing. This process has been [well studied](https://en.wikipedia.org/wiki/Photogrammetry), but usually requires distinct, static features in the raw imagery to localize each image with respect to its neighbors. However, it is infeasible to use this approach when imaging bodies of water, which are oftentimes dynamic and feature-sparse. The [RESL aquatics group](https://robotics.usc.edu/resl/research/1) is working on a new method for orthomosaicing over dynamic landscapes by dropping floating, instrumented [ground control points (GCPs)](https://www.pix4d.com/blog/why-ground-control-points-important) across the target area before the aerial survey.

{% include image-caption.html
    url="/assets/images/orthomosaic-drone-photo.png"
    description="Sample aerial survey image. Beach surveys provide a good analogue since they tend to be feature-sparse. You can see Chris dragging a GCP to simulate movement between photos."
%}

These instrumented ground control points are composed of a large [April tag](https://april.eecs.umich.edu/software/apriltag) and a device that logs GPS and IMU data. Additionally, the imagery from the drone will provide relative position estimates between the drone camera and the GCP.

{% include image-caption.html
    url="/assets/images/orthomosaic-gcp.png"
    description="Ground Control Point hardware. We package this with an external battery in a waterproof container before deploying them."
%}

Surprisingly, we have not found a COTS solution for logging GPS and IMU data at our price range (<$100 per unit), so we had to make our own logger. Our emphasis is on using cheap, easily accessible sensors and improving the solution quality with advanced state estimation techniques. This allows us to use hobbyist-level electronics, specifically a Raspberry Pi with an [Adafruit GPS Hat](https://www.adafruit.com/product/2324) and [BNO055 9-DoF IMU](https://www.adafruit.com/product/2472).

Using a factor-graph solver from the [GTSAM library](https://github.com/borglab/gtsam), we construct a smoothing and mapping problem that uses the odometry from the drone and GCPs, and the visual distance estimates between the drone and GCPs to jointly minimize the error in the pose of the drone and camera. Using the refined pose estimates of the camera allow us to create a much more accurate orthomosiac than if we relied only on the drone's odometry data.

If you have questions about our approach or framework, please email me!

{% include image-caption.html
    url="/assets/images/orthomosaic-beach.jpg"
    description="Sometimes, research means going to the beach!"
%}
