---
layout: page
title: Orthomosaicing for Aquatic Imagery
permalink: /projects/orthomosaic/
---

![Stitched image of the Aukerman dataset](/assets/images/orthomosaic-aukerman.png){:class="img-responsive"}

*This project is currently a work in progress! More information will be provided once we have published.*

Collecting detailed imagery of a survey area often involves flying an aerial vehicle to take multiple top-down pictures and stitch them together in a process called orthomosaicing. This process has been well studied, but requires distinct, static features in the raw imagery to localize the each image with respect to its neighbors. However, it is infeasible to use such features when imaging bodies of water, which is oftentimes dynamic and feature-sparse. The [RESL aquatics group](https://robotics.usc.edu/resl/research/1) is working on a new method for orthomosaicing over dynamic landscapes by dropping floating, instrumented ground control points (GCPs) across the target area before the aerial survey.

![Sample aerial survey image](/assets/images/orthomosaic-beach.jpg){:class="img-responsive"}

These instrumented ground control points log telemetry from a GPS and IMU sensor, which can be used to estimate its pose over time. However, the imagery from the drone will also provide relative position estimates between the drone camera and the GCP.

![Ground Control Point hardware](/assets/images/orthomosaic-gcp.png){:class="img-responsive"}

Surprisingly, we have not found a COTS solution for logging GPS and IMU data at our price range (<$100 per unit), so we had to make our own logger. Our emphasis is on using cheap, easily accessible sensors and improving the solution quality with advanced state estimation techniques. This allows us to use hobbyist equipment, specifically a Raspberry Pi with an [Adafruit GPS Hat](https://www.adafruit.com/product/2324) and [BNO055 9-DoF IMU](https://www.adafruit.com/product/2472).

Using a factor-graph solver from the [GTSAM library](https://github.com/borglab/gtsam), we construct a smoothing and mapping problem that uses the odometry from the drone and GCPs, and the visual distance estimates between the drone and GCPs to jointly minimize the error in the pose of the drone and camera.