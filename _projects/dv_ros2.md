---
title: Event camera ROS2 Integration
description: Implementing a ROS2 driver and integration for the DV Event Camera.
order: 3
teaser_image: /assets/gifs/event_camera.gif
teaser_image_dark: /assets/gifs/event_camera.gif
hero_image: /assets/images/dv_ros2_project_header.png
hero_image_dark: /assets/images/dv_ros2_project_header.png
role: Lead Engineer
stack: ROS2, C++, Python
timeline: 2024
tags:
  - ROS
  - Computer Vision
links:
  - label: GitHub Repo
    url: https://github.com/telios/dv-ros2
---

## The Goal
The ROS drivers for the event cameras from iniVation AG would only support ROS1, and the company had no plans to support ROS2. The goal of this project was to implement a ROS2 wrapper for the DV software suite, enabling seamless integration of the DV Event Camera with ROS2-based robotic systems.

## The How
Features that were implemented in the ROS1 wrapper were ported to ROS2, including:
- Real-time event streaming
- IMU data integration
- Dynamic reconfiguration of camera parameters
- Support for multiple camera models


## The Results

<div align="center" class="image-with-padding">
    <img src="/assets/gifs/event_camera_images.gif" width="80%"/>
</div>
All components available in the ROS1 driver were re-implemented using ROS2 best practices, ensuring compatibility with the latest ROS2 distributions.
The project was open-sourced on GitHub, allowing the robotics community to leverage the capabilities of the DV Event Camera within ROS2 environments.