---
title: Autonomous Exploration with Spot
description: Frontier-Based Autonomous Exploration and Mapping with the Spot robot from Boston Dynamics.
order: 2
teaser_image: /assets/gifs/spot_exploration.gif
teaser_image_dark: /assets/gifs/spot_exploration.gif
hero_image: /assets/images/bachelor_project_header.png
hero_image_dark: /assets/images/bachelor_project_header.png
role: Lead Engineer
stack: ROS1, C++, Python, LiDAR, SLAM
timeline: 2022
tags:
  - Robotics
  - ROS
links:
  - label: GitHub Repo
    url: https://github.com/telios/catkin_ws_spot
  - label: Thesis document
    url: /assets/documents/bachelor_thesis.pdf
---


## The Goal
The objective was to enable **fully autonomous 2D exploration** for the Boston Dynamics Spot robot without human guidance. While Spot features semi-autonomous "Autowalk" (replaying recorded paths), it lacked the ability to enter a completely unknown environment and map it autonomously.

My goal was to build a system that could:
* **Autonomously Map:** Construct a coherent 2D occupancy grid of an unknown room using LiDAR.
* **Navigate Safely:** Plan paths around static obstacles and through narrow doorways.
* **Decide Where to Go:** Algorithmically identify "frontiers" (boundaries between known and unknown space) to maximize information gain.

## The How
I integrated a complete navigation pipeline on the **SpotCORE** payload (an onboard Intel i5 computer) using **ROS 1 (Melodic)**.
* **SLAM (Cartographer):** I utilized **Google Cartographer** for 2D Simultaneous Localization and Mapping. This was chosen over other algorithms (like Gmapping) for its superior loop-closure capabilities (Sparse Pose Adjustment), which are critical for correcting drift during long exploration runs. I configured it to ingest 3D data from a **Velodyne VLP-16 LiDAR**, flattening it into 2D scans for efficient processing.
* **Frontier Exploration:** I used the `explore_lite` package, which runs a Breadth-First Search (BFS) on the occupancy grid to detect frontier edges. It groups these edges and calculates centroids to serve as navigation goals, prioritizing the nearest unexplored areas to minimize travel time.
* **Navigation Stack Tuning:**
    * **Global Planner:** Used `navfn` (Dijkstra) configured to prevent planning through unmapped areas.
    * **Local Planner:** I benchmarked the Dynamic Window Approach (DWA) against **Trajectory Rollout (TRA)**. I found that DWA performed poorly with Spot's specific kinematics, so I optimized the TRA planner for smoother velocity commands.
    * **Costmaps:** I fine-tuned inflation radii to allow the robot to pass through narrow openings (like doorways) that standard configurations would mark as untraversable.

## The Results
<div class="video-container">
    <iframe src="https://www.youtube.com/embed/5NRiSeR9sXQ" allowfullscreen="" frameborder="0">
    </iframe>
</div>
The system was validated in a **real-world experiment** at the TU Vienna Science Center. I tested two scenarios: an empty room and a cluttered room with added barriers.

* **Autonomous Completion:** In both scenarios, Spot successfully identified and reached all frontiers without any human intervention.
* **High Map Quality (Scenario 1):** In the empty room test, the system achieved **99.04% Map Coverage** with a Structural Similarity Index (SSIM) of **0.89** compared to the ground truth (derived from a laser-measured 3D model).
* **Obstacle Handling (Scenario 2):** In the cluttered scenario, the robot successfully navigated around unexpected barriers. While the map coverage dropped to **89.04%** due to some odometry drift causing map compression, the robot successfully completed the exploration mission.
* **Real-Time Loop Closure:** The system demonstrated the ability to recognize previously visited areas and snap the map back into alignment, validating the choice of Cartographer over simpler mapping techniques.