# GoChaseIt - ROS Ball Chaser Robot 🤖⚽

A differential drive robot simulation built with ROS Noetic and Gazebo. The robot autonomously detects a white ball using a camera sensor and drives toward it using a Proportional (P) controller.

![Robot Simulation](https://img.shields.io/badge/ROS-Noetic-blue) ![Gazebo](https://img.shields.io/badge/Simulation-Gazebo-orange) ![Language](https://img.shields.io/badge/C++-11-green)

## 📖 Project Overview
This project consists of two ROS packages working together:

1.  **`my_robot`**: Defines the physical robot and the simulation environment.
    * **URDF/Xacro**: A custom differential drive robot with Lidar and Camera sensors.
    * **Gazebo World**: A custom environment (`perfect.world`) where the robot interacts.
2.  **`ball_chaser`**: Handles the autonomous control logic.
    * **`drive_bot`**: A Service Server C++ node that controls the robot's motor velocities.
    * **`process_image`**: A Service Client C++ node that analyzes camera data to detect the white ball and commands the robot to follow it.

## 🛠️ Prerequisites
* **OS:** Ubuntu 20.04 (Focal Fossa)
* **ROS:** Noetic Ninjemys
* **Simulation:** Gazebo & RViz
* **Build System:** Catkin

## 📂 Directory Structure
```text
/home/workspace/catkin_ws/src/
│
├── my_robot/                      # Package 1: Robot Description & World
│   ├── launch/
│   │   ├── robot_description.launch
│   │   └── world.launch           # Launches Gazebo with 'perfect.world'
│   ├── urdf/
│   │   ├── my_robot.gazebo        # Gazebo plugins (camera, lidar, drive)
│   │   └── my_robot.xacro         # Robot structure and link definitions
│   └── worlds/
│       └── perfect.world          # Custom simulation environment
│
└── ball_chaser/                   # Package 2: Control Logic
    ├── launch/
    │   └── ball_chaser.launch     # Launches drive_bot and process_image nodes
    ├── srv/
    │   └── DriveToTarget.srv      # Service definition (linear_x, angular_z)
    └── src/
        ├── drive_bot.cpp          # Service Server (Motor Command)
        └── process_image.cpp      # Service Client (Image Processing & P-Controller)
