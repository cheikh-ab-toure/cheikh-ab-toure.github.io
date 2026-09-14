---
layout: post
title: MedReach - Robot Hand Teleoperation
description: A computer vision teleoperation system that tracks a user's hand in real time and mirrors the motion onto a simulated 6-DOF robotic hand, built for the Coding Collective at NCAT HackNat 9.0. Secured 2nd Place for innovation out of 10+ competing teams.
skills: 
- Computer Vision
- Python
- Real-Time Control
- Telemetry Systems
- Human-Robot Interaction
main-image: /medreach-logo.png
---

---
# Overview
MedReach is an interactive Python-based application that uses computer vision to track a user's hand in real time. The system detects finger and wrist movement and mirrors it onto a robotic hand with six degrees of freedom for smooth, lifelike motion. Built as a team of 4 for NCAT HackNat 9.0 (Fall 2025), the project was designed around the theme "Teleoperation and Innovation in Health Care Management," aligning with Johnson & Johnson MedTech's focus on enhancing surgical performance through robotic-assisted and digital technologies.

The name combines "Medical" and "Reach" — extending human precision and control into surgical and simulation environments.

## Problem statement: 
Remotely control a robotic arm to position the arm's end effector within a simulation environment, using intuitive hand tracking instead of manual joint-by-joint input.
{% include image-gallery.html images="control-panel-demo.png" height="450" %}

# How it Works
The app runs in-browser and offers two control modes:
- IK (Mimic) Control — tracks and mirrors your hand movement directly; making a fist closes the gripper, opening your hand releases it.
- Manual Joint Control — switches to precise, individual joint-by-joint control for fine adjustments.

Hand tracking runs through the webcam feed, extracting finger and wrist position in real time, which then drives inverse kinematics to position the simulated arm's end effector.

{% include image-gallery.html images="joint-motion-plot.png" height="400" %}

# Telemetry & Recording
Every session can be recorded — the app logs joint angles, end-effector position, and flex amount over time, then exports the data as CSV or JSON. Recorded motion can be reloaded and played back at adjustable speed, which made it possible to review and analyze full motion sequences after each demo rather than only observing live.
