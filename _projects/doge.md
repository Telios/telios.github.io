---
title: DOGE
description: Model-based Reinforcement Learning for Dynamic Obstacle Ground-based Evasion with a quadruped robot.
order: 3
teaser_image: /assets/gifs/doge_in_mujoco.gif
teaser_image_dark: /assets/gifs/doge_in_mujoco.gif
hero_image: /assets/images/doge_project_header.png
hero_image_dark: /assets/images/doge_project_header.png
role: Lead Engineer
stack: ROS2, C++, Python, Mujoco
timeline: 2024
tags:
  - ROS
  - Computer Vision
  - Reinforcement Learning
  - Robotics
  - Deep Learning
links:
  - label: GitHub Repo
    url: https://github.com/telios/doge
---

## The Goal
The objective of **DOGE** was to enable **Solo12**, a quadruped robot, to dynamically detect and evade incoming projectiles in real-time.

Standard evasion systems often rely on heavy computation or traditional frame-based cameras, which suffer from motion blur and higher latency. My goal was to create a highly reactive system that could:
* **Perceive in High-Speed:** Utilize an **event-based camera** to track fast-moving objects with microsecond latency.
* **Learn Dynamic Agility:** Move beyond static path planning by using **Model-Based Reinforcement Learning** to teach the robot agile dodging maneuvers.
* **Operate in Real-Time:** Integrate high-frequency motor control (100Hz) with the vision system.

## The How
I developed a comprehensive framework integrating state-of-the-art AI with custom robotics drivers.

<div align="center" class="image-with-padding">
    <img src="/assets/images/doge_overview.png" width="80%"/>
</div>

* **Model-Based RL (DreamerV3):** I leveraged the **DreamerV3** world model to train the agent in the Mujoco simulation. Unlike model-free approaches, DreamerV3 learns an internal model of the environment, allowing it to imagine future outcomes and learn efficient policies for dodging projectiles with high sample efficiency.
* **Locomotion Controller:** The system controls the Solo12 robot using a deep reinforcement learning-based controller. It accepts high-level velocity commands (forward, lateral, and rotational) and outputs precise joint angles at **100Hz**, ensuring smooth and rapid physical responses.
* **Sim-to-Real Strategy:** I employed **Domain Randomization** during simulation training. This involved varying projectile sizes, speeds, launch distances, and angles, as well as injecting noise into the robot’s state sensors (IMU, joint encoders) to mimic real-world hardware imperfections.

## The Results
The project successfully demonstrated the potential of model-based RL for dynamic quadruped agility.
<div align="center">
  <div class="image-container">
       <img src="/assets/gifs/event_camera_doge.gif" width="70%"/>
         <p>Simulation results from the event-based camera</p>
  </div>
  <div class="image-container">
        <img src="/assets/gifs/doge_in_mujoco.gif" width="70%"/>
          <p>Simulation results in Mujoco</p>
  </div>
</div>


* **Simulation Success:** The DreamerV3 agent successfully learned a robust policy in simulation, capable of consistently dodging incoming projectiles by coordinating body movement and orientation.
* **Open Source Contribution:** A **ROS 2 wrapper** for the event-based camera was released as an open-source tool, facilitating easier integration of neuromorphic vision sensors for the wider robotics community.

<div class="video-container">
    <iframe src="http://www.youtube.com/embed/iKfP1ISdhV8" allowfullscreen="" frameborder="0">
    </iframe>
</div>

* **Sim-to-Real Challenges:** While the policy performed well in simulation, the direct transfer to the physical Solo12 robot faced a significant **sim-to-real gap**. The real-world physics and sensor noise profiles proved distinct enough that the policy requires further refinement.
* **Future Work:** Identifying pathways for bridging this gap include more aggressive domain randomization and sophisticated reward shaping to encourage more stable real-world behaviors.