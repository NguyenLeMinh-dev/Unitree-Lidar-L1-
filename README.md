# 🛰️ Unitree LiDAR L1 — ROS2 Humble Setup Guide

<p align="center">
  <img src="./docs/images/ROS2_logo.png" alt="ROS2 Logo" width="500"/>
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

## 🏗️ Step 4 — Create and Build Your First Workspace

Create a new workspace directory (commonly named ros2_ws):

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
git clone https://github.com/unitree/unitree_lidar_ros2.git
cd ~/ros2_ws
```

Use Colcon to build all packages inside your workspace:

```bash
colcon build --symlink-install
```

After the build process is complete, source the workspace to make ROS2 recognize the new packages:
```bash
source install/setup.bash
```

Run the following command to start the LiDAR driver:
```bash
ros2 launch unitree_lidar_ros2 launch.py
```

You can visualize the LiDAR output using RViz2:
```bash
rviz2 -d src/unitree_lidar_ros2/rviz/view.rviz 
```
In RViz2, you can see the LiDAR output in the "PointCloud2" topic.


![img](./docs/images/lidar_unitree_l1.png)



# 🛰️ Point-LIO — SLAM Guide for Unitree LiDAR L1

Point-LIO is a LiDAR–Inertial SLAM framework that performs direct point-to-map optimization instead of relying on feature extraction. Unlike FAST-LIO, which uses planar features and IKF updates, Point-LIO treats every LiDAR point as a valid measurement for state estimation.

This results in a SLAM system that is:

More accurate in complex or unstructured environments

More robust when planar/edge features are scarce

Better suited for high-resolution LiDAR sensors (e.g., Unitree L1, Ouster, Velodyne)

## 📘 Overview
This document provides a step-by-step guide to set up and run the **Point-LIO** with **ROS2 Humble** on **Ubuntu 22.04 LTS**.

## Pack Requirements
- For ROS2 Humble
```bash
sudo apt-get install ros-humble-pcl-ros
sudo apt-get install ros-humble-pcl-conversions
sudo apt-get install ros-humble-visualization-msgs
```

- Eigen
```bash
sudo apt-get install libeigen3-dev
```

- Clone the repository and colcon build:
```bash
mkdir -p catkin_point_lio_unilidar/src
cd catkin_point_lio_unilidar/src
git clone https://github.com/dfloreaa/point_lio_ros2.git
cd ..
colcon build --symlink-install
source install/setup.bash
```

## Run the Point-LIO
```bash
cd ~/catkin_point_lio_unilidar
source install/setup.bash
ros2 launch point_lio mapping_unilidar_l1.launch.py
```

## Results
![img](./docs/images/lidar_fastLIO.png)