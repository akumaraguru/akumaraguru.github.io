---
layout: page
title: Automated door opener
permalink: /projects/leaky/
---

{% include youtubePlayer.html id="mJVWrDmWAfI" %}

[source code](https://github.com/akumaraguru/leaky)

In order to provide keycard access to a common room, I helped develop a motorized door opener that authenticates users via RFID tags.

## System

The door opener was designed to be non-obtrusive, fitting inside a bookshelf adjacent to the door. Users could tag their cards to a pcProx card reader, which reads the RFID code to the central computer, a Beaglebone Black. The computer authenticates the RFID code against an encrypted database maintained on a cloud server.

## Actuation

Once authenticated, the system drives a single-joint arm powered by a CIM motor to rotate and latch open the door. The challenge here is that the door bar requires a relatively heavy load before latching open, so the motor must be heavily geared down. However, applying too much force to the door bar will damage the door, or the door opener itself.

Prior iterations of the door opener simply ran the arm in open-loop until a limit switch was triggered. However, the excessive force ended up destroying the limit switch over time.

To solve this, I equipped a load cell on the edge of the bar to measure the force applied to the door bar. This allows us to use a closed-loop feedback system to control how much force to apply to the door bar. I wrote a PID library in Python that automatically adjusts its gains in response to variable sample times from the non-real time OS. The Beaglebone is equipped with two realtime compute units, but for the purpose of portability, we chose to not utilize them here. Limit switches were also placed along the arm to sense unintended collisions, which would trigger an immediate retraction.

This approach greatly improved the reliability of the system, and absolved us from having to replace the limit switch every few months.
