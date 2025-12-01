# **SLAM with 3D LiDAR Laser Scan**

This repository provides a customized extension of **`clearpath_nav2_demos`** that enables launching SLAM and localization **directly from a 3D LiDAR laser scan**—without manually specifying arguments. The system automatically detects and utilizes the `3dLidar_scan` topic.

This setup is optimized for **Clearpath Robotics platforms**, including the **J100** and **A300** models.

---

## **1. Install Clearpath Navigation Demos**

Make sure your system is updated and install the base package:

```bash
sudo apt-get update
sudo apt-get install ros-<distro>-clearpath-nav2-demos
```

Replace `<distro>` with your ROS 2 distribution, e.g., `jazzy`, `humble`, etc.

---

## **2. Create an Overlay Workspace**

Create a workspace under your home directory:

1. Create a ROS 2 workspace:

   ```bash
   mkdir -p ~/ws_name/src
   cd ~/ws_name/src
   ```

2. Clone this repository **inside your `clearpath_nav2_demos` package**:

   ```bash
   mkdir clearpath_nav2_demos/src -p
   cd clearpath_nav2_demos/src
   git clone <this-repo-url> .
   ```

3. Return to the workspace root and build:

   ```bash
   cd ~/ws_name
   sudo apt install python3-colcon-common-extensions
   colcon build
   ```

---

## **3. Source Your Workspace**

Either source manually each session:

```bash
source ~/ws_name/install/setup.bash
```

Or automatically source it by editing your `.bashrc`:

```bash
gedit ~/.bashrc
```

Add:

```bash
source /opt/ros/<distro>/setup.bash
source ~/ws_name/install/setup.bash
```

---

## **4. Launch the Simulation and SLAM**

Use the following sequence to start simulation, navigation, SLAM, and RViz2 visualization:

### **Start Gazebo Simulation**

```bash
ros2 launch clearpath_gz simulation.launch.py setup_path:=/home/dsandeshh/clearpath/
```

### **Start Nav2**

```bash
ros2 launch clearpath_nav2_demos nav2.launch.py use_sim_time:=true setup_path:=/home/dsandeshh/clearpath/
```

### **Start SLAM with 3D LiDAR**

```bash
ros2 launch clearpath_nav2_demos slam.launch.py use_sim_time:=true setup_path:=/home/dsandeshh/clearpath/
```

### **Start RViz2 Visualization**

```bash
ros2 launch clearpath_viz view_navigation.launch.py namespace:=/j100_0000 use_sim_time:=true
```

---

## **You're Good to Go!**

Your simulation environment should now be running with **SLAM + Navigation + Visualization** fully configured for 3D LiDAR input on Clearpath robots.
