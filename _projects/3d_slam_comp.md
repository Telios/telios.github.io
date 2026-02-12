---
title: 3D SLAM Comparison
description: A comparison of different 3D SLAM algorithms for mobile robots.
order: 3
teaser_image: /assets/gifs/3dslam_comparison.gif
teaser_image_dark: /assets/gifs/3dslam_comparison.gif
hero_image: /assets/images/3dslam_comp_header.png
hero_image_dark: /assets/images/3dslam_comp_header.png
role: Lead Engineer
stack: ROS1, Python, tmux, Docker, LiDAR
timeline: 2023
tags:
  - ROS
  - Robotics
  - Computer Vision
links:
  - label: GitHub Repo
    url: https://github.com/telios/3dslam_comparison
---

## The Goal
The objective of this project was to identify the optimal **Front-End LiDAR Odometry** system to integrate with **LAMP** (Large Scale Autonomous Mapping and Positioning), a robust back-end SLAM system developed by the NASA JPL NeBula team.

Navigating complex, multi-story environments with the Boston Dynamics Spot robot requires a SLAM front-end that is both highly accurate and computationally efficient. My goal was to:
* **Benchmark Performance:** Rigorously test five leading LiDAR odometry algorithms (FAST-LIO, FASTER-LIO, DLO, DLIO, LOCUS).
* **Quantify Accuracy:** Compare the resulting maps against sub-centimeter accuracy ground truth data from a **Riegl VZ-400i** laser scanner.
* **Optimize for Compute:** Determine which solution offers the best trade-off between CPU/RAM usage and map quality for deployment on constrained onboard hardware.

## The How
I implemented a benchmarking framework to evaluate these algorithms side-by-side using real-world data.

<div align="center">
  <div class="image-container">
       <img src="/assets/gifs/riegl_registration.gif" width="70%"/>
         <p>Recording of ground truth pointcloud</p>
  </div>
  <div class="image-container">
        <img src="/assets/gifs/fast-lio.gif" width="80%"/>
          <p>Real-time 3D LiDAR odometry with FAST-LIO</p>
  </div>
</div>
* **Data Collection:** I recorded custom datasets using a **Boston Dynamics Spot** robot equipped with **Ouster OS-128** and **Velodyne VLP-16** LiDARs in challenging multi-story environments.
* **System Integration:** I created a unified Docker/tmux-based build system to manage the complex dependencies of multiple competing SLAM research codebases, ensuring reproducible builds on ROS Melodic.
* **Ground Truth Generation:** I used a survey-grade **Riegl VZ-400i** terrestrial laser scanner to create millimeter-accurate reference maps of the test environments. 
* **Automated Profiling:** I developed Python scripts to automatically track real-time CPU and RAM usage for each algorithm during execution.
* **Accuracy Analysis:** I utilized **CloudCompare** to perform Cloud-to-Cloud (C2C) distance calculations, generating heatmaps of drift and error by aligning the SLAM output with the Riegl ground truth.

## The Results
The comprehensive benchmark provided clear, data-driven recommendations for the final system architecture.

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/3nIMLWOj0Ts" allowfullscreen="" frameborder="0">
    </iframe>
</div>

* **Top Performers:** **DLO (Direct LiDAR Odometry)** and **FAST-LIO** emerged as the best candidates. They demonstrated the lowest computational overhead while maintaining high accuracy.
* **Accuracy Validation:** Both DLO and FAST-LIO produced maps with minimal deviation from the Riegl ground truth, successfully closing loops in multi-story traversals.
* **Resource Efficiency:** While **DLIO** (Direct LiDAR-Inertial Odometry) offered excellent accuracy, its memory usage was prohibitively high for the target hardware.
* **System Recommendation:** The final recommendation was to deploy **DLO** or **FAST-LIO** as the lightweight onboard front-end on Spot, offloading the heavy **LAMP** back-end optimization to a remote base station to maximize performance.