# Introdution to LiDAR
*Maodian Huang*

## What is LiDAR?
> What do you get when you add wings to a LiDAR scanner?

> "GLiDAR!"

**LiDAR**: Light Detection and Ranging

- a remote sensing technology that uses laser light to measure distances and create high-resolution 3D maps or point clouds of the surrounding environment.

- distances are calculated by first having a LiDAR system emit laser pulses towards an area. When the laser pulses encounter objects in the environment, they reflect back towards the LiDAR sensor.

![](/Img/lidar_working.png)

### What are point clouds?
> They're like clouds, but made out of points LMAO!

**Point Clouds**: Collections of 3D data points that represent the spiral coordinates of objects or surfaces in a three-dimensional space. Each point in a point cloud is (usually) defined by its X, Y, Z coordinates, capturing the position of a specific location in the envirionment.

![](/Img/PointCloud1.jpg)

### Advantages of LiDAR

- High Precision and Accuracy

- All-Weather Capability

- Long Distance

- etc.

### Application of LiDAR

- **Autonomous Vehicles**: perceive the surrounding vehicles, detect obstacles, assist navigation.

- **Mapping and Surveying**: create detailed topographic maps, digital models(building, landscapes)

- **Remote sensing**: study vegetation, monitor forest health etc

- etc.

- **MOST IMPORTANTLY, widely used in localization and navigation algorithms for robots competing in the Robomaster competitions**

## How does LiDAR work?

1. get a supported hardware

There are a wide variety of LiDAR sensors available from companies such as Velodyne, Livox, Ouster etc.

2. preprocessing

A series of steps to clean, filter, and prepare the raw LiDAR data for further analysis and applications. 

Common operations are: downsampling, denoising etc.

3. labeling, segmentation and detection

Helps you organize, categorize the data. Removing parts of the PointCloud that's irrelevent.

4. calibration and sensor fusion

When using multiple sensors, the sensors must be calibrated to work properly together. For example, we need to align the coordinate systems of multiple sensors through transformation and synchronization. 

5. navigation and mapping

Mapping is the process of building a map of the environment around an autonomous system. 

Simultaneous localization and mapping(SLAM): a system, typically a robot or vehicle, to simultaneously build a map of its environment while determining its own position within that map.

To put it simply, iteratively performing mapping and localization as the robot moves through the environment.

## How does LiDAR, really, work?
> All of this just works! &nbsp; &nbsp; &nbsp; - Todd Howard

### A Quick Taste

![](/Img/PointCloud2.jpg)

Below is an example demonstration

We'll be using a Livox Mid 70 LiDAR sensor for demonstration.

### Connecting to the Computing Device

### Connect with ROS, with a driver package

[Livox_Ros_Driver](https://github.com/Livox-SDK/livox_ros_driver)

A ROS package specially used to connect LiDAR sensors.

Encouraged to attempt an installation on your own hardware. All instructions are (often) listed on the readme file in the github page

#### an important concept: RTFM

RTFM stands for: Read the F\*\*\*\*\*\* manual

typically used to reply to a basic question where the answer is easily found in the documentation.

Serves as a reminder that consulting the available documentation is often the most efficient and accurate way to find answers to basic questions.

### Run the localization & navigation algorithm 

The package we'll be using in the demonstration: [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init)

### Configure RVIZ
*a lot of packages contains launch files that will launch rviz with its included preset configuration files*

#### RVIZ
A built-in visualization tool in ROS (Robot Operating System) that allows users to visualize and interact with various sensor data, robot models, and other information in a 3D environment.

Some important features include:
1. Visualizing sensor data(obviously)
2. Robot visualization
3. Interactive Markers
4. Coordinate Frames
5. Configuration and Customization
6. Debugging and Analysis

Comprehensive user guide: [http://wiki.ros.org/rviz/UserGuide](http://wiki.ros.org/rviz/UserGuide)

## How to debug?
![](/Img/works.png)

### Mindset
- Fix the Problem. Not the Blame
- Don't Panic
- The system is NOT broken
- Don't Assume It - Prove It

### Quick Revision on some ROS operations
**What commands do I need when**:

- I need to view all active ROS nodes?

- I need to view all the current topic names?

- I need to see the contents sent to the topic in realtime?

- I need to view the specific details of a topic? The message type it's sending, for example.

- I need to view the structure of a ROS message?

- I need to check if a node is alive?

- I need to publish a message to a topic?

## How to record and play back data?
> With bags! And it doesn't cost you thousands of dollars either!


### Rosbag
ROS has a built-in system that allows you to record data from a running ROS system into a .bag file, it can then be used to play back the data to produce similar behaviour in a running system.

### Recording data

1. Launch the ROS nodes and topics you want to record
   ```
   roscore
   rosrun turtlesim turtlesim_node
   rosrun turtlesim turtle_teleop_key
   ```
2. Choose a directory to save your .bag file and move to that directory in a terminal
   ```
   mkdir ~/bagfiles
   cd ~/bagfiles
   ```
3. Record 
#### Record all published topics
	```
	rosbag record -a
	```
   
#### Record a subset of the data
	```
	rosbag record -O subset /turtle1/cmd_vel /turtle1/pose
	```
### Examining and playing the bag file

see the specific details about the bag file
```
rosbag info <bagfile>
```

replay the bag file
```
rosbag_play <bagfile>
```





