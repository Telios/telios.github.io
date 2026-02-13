---
title: Digital Twin in Isaac Sim
description: Creating a digital twin of a Staubli robotic arm in NVIDIA Isaac Sim for simulation and testing.
order: 5
teaser_image: /assets/gifs/hiro_card_gif_staubli.gif
teaser_image_dark: /assets/gifs/hiro_card_gif_staubli.gif
hero_image: /assets/images/staubli-isaac-sim_header.png
hero_image_dark: /assets/images/staubli-isaac-sim_header.png
role: Lead Engineer
stack: ROS1, ROS2, NVIDIA Isaac Sim, Python, URDF, USD
timeline: 2024
tags:
  - ROS
  - Robotics
  - Computer Vision
links:
  - label: GitHub Repo
    url: https://github.com/telios/staubli-isaac-sim
---

## The Goal
To modernize the control and perception workflow for a Stäubli TX2-60L industrial robot. The objective was to create a safe, high-fidelity **Sim-to-Real** environment that bridges legacy control systems with next-generation, GPU-accelerated computer vision (ROS2).

## The How
* **Simulation:** Utilized **NVIDIA Isaac Sim** to create a photorealistic twin of the robot and environment for risk-free testing.

<div align="center" class="image-with-padding">
    <img src="/assets/images/staubli_system_overview_ros1.png" width="80%"/>
</div>

* **Hybrid Architecture:** Engineered a bridge between **ROS1** (for robust hardware control via MoveIt and VAL3 drivers) and **ROS2** (for modern perception).
* **Zero-Copy Performance:** Implemented the **ROS NITROS bridge** to transfer high-bandwidth sensor data between ROS1 and ROS2 with zero-copy overhead, enabling the use of **YOLOv8** and DetectNet for real-time object detection.
* **DevOps:** Fully containerized the complex environment using **Docker** and **tmuxp**, ensuring reproducible deployments across GPU workstations.

### The Results

<div align="center">
  <div class="image-container">
        <img src="/assets/gifs/isaac_sim_moveit_ros1.gif" width="89%"/>
          <p>Digital twin of the Stäubli TX2-60L in NVIDIA Isaac Sim</p>
  </div>
  <div class="image-container">
       <img src="/assets/gifs/staubli_real.gif" width="72%"/>
         <p>Movement of the Stäubli TX2-60L in real life</p>
  </div>
</div>

* Achieved seamless motion planning and execution on both the virtual simulation and physical hardware, validating the Sim-to-Real pipeline.

<div align="center" class="image-with-padding">
    <img src="/assets/gifs/yolov8.gif" width="70%"/>
</div>

* Successfully integrated a real-time object detection loop that influences robot behavior without adding latency to the control system.
* Created a portable, modular development environment that isolates dependencies for both the simulation and the hardware drivers.