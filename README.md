# 🛰️ Unitree LiDAR L1 — ROS2 Humble Setup Guide

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/3/3a/ROS_logo.svg" alt="ROS2 Logo" width="120"/>
</p>

<p align="center">
  <b>Quick setup guide for integrating the Unitree LiDAR L1 with ROS2 Humble on Ubuntu 22.04 LTS.</b>
</p>

---

## 📘 Overview

This document provides a step-by-step guide to set up and run the **Unitree LiDAR L1** with **ROS2 Humble**.  
You will install ROS2, set up Colcon, configure the environment, and launch the LiDAR node for testing.

---

## 🚀 Step 1 — Install ROS2 Humble

Install the **ROS2 Humble** distribution on **Ubuntu 22.04 LTS** following the official instructions:

🔗 [ROS2 Humble Installation Guide](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)

After installation, verify that ROS2 was installed successfully:

```bash
echo $ROS_DISTRO
```
Expected Output:
```bash
humble
```

## 🧩 Step 2 — Install Colcon Build

Colcon is the build tool used in ROS2 workspaces. Install it using the command below:

```bash
sudo apt install python3-colcon-common-extensions
```

For more details, see the official documentation: https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html

## ⚙️ Step 3 — Configure the ROS2 Environment

### Option 1 — Using echo
```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```
### Option 2 — Editing .bashrc manually
```bash
nano ~/.bashrc
```
Then add this line at the end of the file: ``source /opt/ros/humble/setup.bash`` 

Save and exit the editor: ``Ctrl + O, Enter, Ctrl + X``

Apply the new configuration: ``source ~/.bashrc``


