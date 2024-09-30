---
layout: default  # Or another layout if you have one
title: Data Format
permalink: /format/ 
---

# Sensor Configuration
- **Stereo Camera:** Custom Underwater Stereo Camera
- **Doppler Velocity Log:** WaterLinked A50 DVL
- **IMU:** MICROSTRAIN 3DM-GX5-AHRS IMU
- **Depth Sensor:** Blue Robotics Bar 30 Pressure/Depth

The sensor frames are defined as follows:

<img src="{{ site.baseurl }}/images/sensor_side.PNG" alt="Sensor frames side view" width="350">
<img src="{{ site.baseurl }}/images/sensor_top.PNG" alt="Sensor frames top view" width="350">

# Data Format
All data is provided by ROS bag and raw data associated with parameter YAML files. 

## ROS Bag

| **Topic**                                           | **Type**                             | **Description**                            |**HZ**|
|-----------------------------------------------------|--------------------------------------|--------------------------------------------|----|
| /camera/left/<br>image_dehazed/compressed             | `sensor_msgs/CompressedImage`        | Left image from the stereo cameras.        | 20 |
| /camera/right/<br>image_dehazed/compressed            | `sensor_msgs/CompressedImage`        | Right image from the stereo cameras.       |20 |
| /imu/data                                         | `sensor_msgs/Imu`                    | IMU data.                                  | 333 |
| /DVL/data                                         | `waterlinked_a50_ros_driver/DVL`     | DVL data.                                  | 5 |
| /depth/data                                       | `nav_msgs/Odometry`                  | Depth data from pressure sensor.           | 30 |
| /apriltag_slam/GT                                 | `nav_msgs/Odometry`                  | GT pose provided by AprilTag SLAM.         | 20 |


## Raw Data
In addition to the ROS bag files, the raw data is also provided in a folder structure. The raw data includes the images from the stereo camera, the depth data from the pressure sensor, the DVL data, the IMU data, and the GT data. An example of folder structure of Strcture\_Easy sequence is shown as follows:
![file_structure]({{ site.baseurl }}/images/structure.png)

# Parameter file
The parameter files provide the camera intrinsic parameters and extrinsic parameters between the sensors in YAML format.

```
#Camera Intrinsics
Camera.fx: 655.0
Camera.fy: 655.0
Camera.cx: 306.0
Camera.cy: 256.0

# stereo baseline times fx
Camera.bf: 78.89165891925023

# Sensor Extrinsic between IMU and Camera
T_imu_camera: !!opencv-matrix
  rows: 4
  cols: 4
  dt: f
  data: [ -0.0165,   -0.0175,   -0.9997,   -0.211687435,
          -0.0106,    0.9998,   -0.0173,    -0.097259169,
          0.9998,    0.0103,   -0.0167,    -0.056238089,
          0,  0,   0,    1 ]

# Sensor Extrinsic between DVL and Camera    
T_dvl_camera: !!opencv-matrix
  rows: 4
  cols: 4
  dt: f
  data: [ -0.0030,    0.0292,    0.9996,   0.132344740,
          0.9995,    0.0328,    0.0021,    0.032085643,
          -0.0327,    0.9990,   -0.0293,    -0.240100175,
          0,  0,   0,    1 ]

          
```