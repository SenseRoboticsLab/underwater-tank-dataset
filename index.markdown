---
layout: default
title: Datase
---

# Dataset


## Sensor Configuration
- **Stereo Camera:** Custom Underwater Stereo Camera
- **Doppler Velocity Log:** WaterLinked A50 DVL
- **IMU:** MICROSTRAIN 3DM-GX5-AHRS IMU
- **Depth Sensor:** Blue Robotics Bar 30 Pressure/Depth

The sensor frames are defined as follows:

<img src="{{ site.baseurl }}/images/sensor_side.PNG" alt="Sensor frames side view" width="350">
<img src="{{ site.baseurl }}/images/sensor_top.PNG" alt="Sensor frames top view" width="350">

## Environment Set Up

![Overview]({{ site.baseurl }}/images/tank_overview.png)

WaveTank dataset provides sequences of varying difficulty that represent various underwater conditions. Moreover, a fiducial-marker-based SLAM system designed to provide high-accuracy 6 DoF pose ground truth data, enabling rigorous evaluation and comparison of underwater SLAM algorithms.

## Data Format
All data is provided by ROS bag and raw data associated with parameter YAML files. 

### ROS Bag
The topics information are as follows:
- **/camera/left/image\_dehazed/compressed:sensor\_msgs/CompressedImage** Left image from the stereo cameras.
- **/camera/right/image\_dehazed/compressed:sensor\_msgs/CompressedImage** Right image from the stereo cameras.
- **/imu/data:sensor\_msgs/Imu** IMU data.
- **/DVL/data:waterlinked\_a50\_ros\_driver/DVL** DVL data.
- **/depth/data:nav\_msgs/Odometry** Depth data from pressure sensor.
- **/apriltag\_slam/GT:nav\_msgs/Odometry** GT pose provided by AprilTag SLAM.

### Raw Data
In addition to the ROS bag files, the raw data is also provided in a folder structure. The raw data includes the images from the stereo camera, the depth data from the pressure sensor, the DVL data, the IMU data, and the GT data. An example of folder structure of Strcture\_Easy sequence is shown as follows:
![file_structure]({{ site.baseurl }}/images/structure.png)

### Parameter file
The parameter files provide the camera intrinsic parameters and extrinsic parameters between the sensors in YAML format.




## Publication
Our work is published in the paper titled _"Tank Dataset: An Underwater Multi-Sensor Dataset for SLAM Evaluation"_ You can find the paper [here]().

Please cite our paper, if you use our data for your research:


## Download
You can download the dataset on our [Download page](/download/). 
