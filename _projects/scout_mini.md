---
title: Fast short-range position control with DRL
description: Developing a Deep Reinforcement Learning agent for precise position control of a holonomic mobile robot in simulation.
order: 4
teaser_image: /assets/gifs/training_scout_mini.gif
teaser_image_dark: /assets/gifs/training_scout_mini.gif
hero_image: /assets/images/scout_mini_header.png
hero_image_dark: /assets/images/scout_mini_header.png
role: Lead Engineer
stack: NVIDIA Isaac Sim, Isaac Lab, Python, PyTorch
timeline: 2024
tags:
  - Deep Learning
  - Robotics
  - Reinforcement Learning
links:
  - label: GitHub Repo
    url: https://github.com/telios/scout_mini_project
---

## The Goal
To develop a robust Deep Reinforcement Learning (DRL) agent capable of navigating a holonomic mobile robot (**Scout Mini**) to randomized target poses in a 3D environment. The objective was to achieve high-precision positioning (error < 5cm) and orientation (error < 1°) while minimizing travel time.

## The How
* **Simulation Framework:** Leveraged **NVIDIA Isaac Lab** and **Isaac Sim** to create a high-fidelity 3D training environment.
* **Parallel Training:** Utilized massive parallelism by training **4096 environments simultaneously** on an NVIDIA RTX 3090, allowing for rapid data collection and iteration.

<div align="center">
  <div class="image-container">
        <img src="/assets/gifs/training_scout_mini.gif" width="80%"/>
          <p>Training of the Scout Mini DRL agent in NVIDIA Isaac Sim</p>
  </div>
  <div class="image-container">
       <img src="/assets/gifs/result_agent.gif" width="83%"/>
         <p>Movement of the trained Scout Mini agent in simulation</p>
  </div>
</div>

* **State Space:** Engineered an observation vector consisting of relative goal position, orientation difference, current velocity, and previous actions to ensure stable convergence.



## The Results

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/Aq6By3qwjZ4" allowfullscreen="" frameborder="0">
    </iframe>
</div>

* **Rapid Convergence:** The agent converged to a stable mean reward in approximately **400 epochs**, with a total training time of just **14 minutes**.
* **High Precision:** Achieved an average distance error of **2.68 cm** (surpassing the 5 cm threshold) and a yaw error of **0.0004°** (surpassing the 1° threshold).
* **Efficiency:** The robot successfully reaches random goals within a 4-meter radius in an average of **2.98 seconds**.