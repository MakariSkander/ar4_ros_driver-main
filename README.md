# 🦾 AR4 Robotic Arm: Integration and Control

<p align="center">
  <img src="Images/3D CAD Assembly.png" alt="AR4 robotic arm 3D CAD assembly" width="400">
</p>

Integration and control of a 6-axis **AR4 robotic arm** (Annin Robotics): stepper motors and drivers, embedded controllers, limit switches, gripper, and ROS-based control and visualization.

Project carried out during my internship at **SOTMO** (Tunisia, February – July 2026).

## My work

- Integrated the electronics of the arm: Teensy 4.1 and Arduino Mega boards, DM542A stepper drivers, stepper motors, limit switches and gripper
- Wired and configured the STEP/DIR control of each joint
- Set up the ROS workspace to visualize and control the arm (URDF/Xacro model, RViz)
- Integrated an NVIDIA Jetson Nano with a camera for object analysis
- Tested and troubleshot the full system step by step: wiring, configuration, calibration and motion

## Hardware

| Component | Role |
|---|---|
| AR4 robotic arm | 6-axis arm with gripper |
| Teensy 4.1 | Main controller: stepper motors, encoders, limit switches |
| Arduino Mega / Nano | Gripper servo and I/O |
| DM542A drivers | Stepper motor drivers (STEP/DIR signals) |
| Stepper motors | Joint actuation |
| Limit switches | Homing and calibration of each joint |
| NVIDIA Jetson Nano + camera | Object analysis |

## Software

- **ROS 2** (Jazzy): `ros2_control`, MoveIt 2, RViz, Gazebo
- **URDF / Xacro** robot model
- **C++** hardware interface, **Arduino** firmware for the Teensy and the Nano
- Linux (Ubuntu), CMake, Git, Docker

## Repository structure

| Folder | Content |
|---|---|
| `_ar4_description/` | Robot model (URDF/Xacro) and 3D meshes for each AR4 version |
| `_ar4_driver/` | ROS 2 hardware interface that talks to the Teensy and the Arduino Nano |
| `_ar4_firmware/` | Firmware for the Teensy 4.1 (`AR4_teensy`) and the Arduino Nano gripper board (`AR4_nano`) |
| `_ar4_moveit_config/` | MoveIt 2 configuration: motion planning, joint limits, kinematics |
| `_ar4_gazebo/` | Gazebo simulation |
| `example_files/` | Simple pick-and-place example in C++ |
| `docs/` | Gripper overcurrent protection: explanation and schematic |

## Getting started

```bash
# In a ROS 2 workspace
cd ~/ar4_ws/src
git clone https://github.com/MakariSkander/ar4_ros_driver-main.git
cd ~/ar4_ws
rosdep install --from-paths src --ignore-src -r -y
colcon build
source install/setup.bash

# Simulation with MoveIt and RViz (no hardware needed)
ros2 launch annin_ar4_moveit_config demo.launch.py
```

To control the real arm, flash `_ar4_firmware/AR4_teensy/AR4_teensy.ino` to the Teensy 4.1, then start the driver:

```bash
ros2 launch annin_ar4_driver driver.launch.py
```

## Robotics concepts

Robot geometry · forward and inverse kinematics · joint and motion control · homing with limit switches · gripper control · hardware/software integration

## Credits

- The ROS 2 packages and firmware in this repository are based on the open-source [ar4_ros_driver](https://github.com/ycheng517/ar4_ros_driver) project by Yifei Cheng and contributors, under the MIT license (see [`LICENSE`](./LICENSE)).
- The AR4 robotic arm is designed by [Annin Robotics](https://www.anninrobotics.com/).

## Author

Skandar Makari · [GitHub](https://github.com/MakariSkander)
