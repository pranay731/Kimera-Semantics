# Kimera-Semantics on MIT ADE20K Dataset
### Forked from Kimera-Semantics by MIT SPARK lab, implementaion over MIT ADE20K Dataset.

Reconstructs 3d environment with semantics containing 150 classes of ADE20K dataset. Requires color, depth and segmented images as input. "README_SPARK.md" should be refered for more info.

## 1. Installation

### A. Prerequisities

- Install ROS by following [our reference](./kimera/docs/ros_installation.md), or the official [ROS website](https://www.ros.org/install/).

- Install system dependencies:
```bash
sudo apt-get install python-wstool python-catkin-tools  protobuf-compiler autoconf
# Change `melodic` below for your own ROS distro
sudo apt-get install ros-melodic-cmake-modules
```

### B. Kimera-Semantics Installation

Using [catkin](http://wiki.ros.org/catkin):

```bash
# Setup catkin workspace
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin init
catkin config --extend /opt/ros/melodic
catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release
catkin config --merge-devel

# Add workspace to bashrc.
echo 'source ~/catkin_ws/devel/setup.bash' >> ~/.bashrc

# Clone repo
cd ~/catkin_ws/src
git clone https://github.com/pranay731/Kimera-Semantics-on-ADE20K.git

# Install dependencies from rosinstall file using wstool
wstool init # Use unless wstool is already initialized

# For ssh:
wstool merge Kimera-Semantics/kimera/install/kimera_semantics_ssh.rosinstall
# For https:
#wstool merge Kimera-Semantics/kimera/install/kimera_semantics_https.rosinstall

# Download and update all dependencies
wstool update
```

Finally, compile:

```bash
# Compile code
catkin build kimera

# Refresh workspace
source ~/catkin_ws/devel/setup.bash
```

## 2. Usage

  1. Launch required packages for:
      - Camera color and depth input
      - Semantic Segmentation input
      - Odometry and tf frames
  

  2. Launch file :
      - left_cam_info_topic -> color camera_info topic
      - left_cam_topic -> color image_raw topic
      - left_cam_depth_topic -> depth image_raw topic
      - left_cam_segmentation_topic -> segmented color image_raw on ADE20K classes

  3. Launch Kimera-Semantics:

  ```bash
  roslaunch kimera_semantics_ros kimera_semantics_realsense.launch
  ```

  4. Launch rviz for visualization:

  ```bash
  source ~/catkin_ws/devel/setup.bash
  rviz -d $(rospack find kimera_semantics_ros)/rviz/kimera_semantics_realsense.rviz
  ```

If runing in a Gazebo simulation, use 'kimera_semantics_gazebo' launch and rviz files.

