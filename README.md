# Turtlebot
This is project inspired from the Mathworks Matlab - Excellence in Innovation Repository :
https://github.com/mathworks/MathWorks-Excellence-in-Innovation.git.

## Installation :
You can install turtlebot by following
[Turtlebot3 Installation Tutorial.](https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/)

SLAM Simulation
1. Launch Simulation World -<br>
`$ export TURTLEBOT3_MODEL=burger`<br>
`$ roslaunch turtlebot3_gazebo turtlebot3_world.launch`: 
3. Run SLAM Node -<br>
`$ export TURTLEBOT3_MODEL=burger`<br>
`$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping`
4. Run Teleoperation Node -<br>
  `$ export TURTLEBOT3_MODEL=burger`<br>
`$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`
6. Save Map -<br>
`$ rosrun map_server map_saver -f ~/map`

## Description :
The project is an experiment of finding the shortest path to a given set of start and end points namely waypoints using RRT* Path planning algorithm in a rough terrain and then deploying these waypoints on the turtlebot robot. Mainly the tools used were MATLAB for generating the waypoints using a map of the given environment in pgm file, further more feeding this shortest path to a robot in Gazebo Ros simulation using the simulink model.

## Procedure :
Following are the steps taken for running this project -
1. Below is a rough terrain environment suitable for the application - source: husky clearpath , husky playpen environment :
![environment](https://github.com/Autonomousanz/Autonomous-Navigation-in-Rough-Terrain/blob/master/Pictures/huskeyplaypath.png)

2. Launching the robot in this environment using the launch file which contains the world file location in the catkin workspace 
3. Generate a pgm file through slam mapping of this environment, the pgm file of the chosen environment is already available by default in the husky clearpath installation.

![map pgm file](https://github.com/Autonomousanz/Autonomous-Navigation-in-Rough-Terrain/blob/master/Pictures/map.pgm)

4. Once the pgm file is available, use a matlab mlx script RRT planner to generate a path using RRT* algorithm. One major challenge is to transform the coordinates of gazebo world with the exact coordinates from pgm file format.

![RRT planner path generated](https://github.com/Autonomousanz/Autonomous-Navigation-in-Rough-Terrain/blob/master/Pictures/Picture1.jpg)

5. A roslocation.cpp script was used to establish a correlation with map coordinates on the pgm file and the gazebo simulated environment
6. After creating the waypoints, the last point is goal of the trajectory which needs to be transformed back into gazebo coordinates. The mathworks path following with obstacle avoidance slx file takes this goal point as input to then generate the corresponding velocity upon connection with gazebo simulation. a rosinit command must be initialized in the command line of matlab to establish ros master connection with the turtlebot.
7. The robot then traverses the given path and goal set in Gazebo environment after the simulink model runs successfully.

## Results :

![Runtime](https://github.com/Autonomousanz/Autonomous-Navigation-in-Rough-Terrain/blob/master/Videos/run.gif)

## Conclusion :
Autonomous Navigation using RRT* path planning algorithm was achieved using turtlebot3 burger model in Gazebo ROS simulated environment. The scope of this project was limited to small rough terrain environment and can be further extended with additional optimizations such as testing dynamic obstacle avoidance cases and other worst case scenarios. The outcome of this analysis was an introductory study of autonomous navigation of robots in a rough terrain concepts and its workings using MATLAB and ROS GAZEBO environments. 

## Future Work :

There are following improvement points which needs to considered for further optimizing this model:

1. Using an actual off road terrain robot such as husky in an agricultural land which is already available in clearpath robotics git will prove to be more significant contribution for further study and analysis.
2. Currently this project experiments using pure pursuit controller,optimizing the control of the robot to overcome the troughs of the environment by accounting uneven ground can be another approach that needs to be further investigated.

## Credits

We are thankful to the support of mentors and advisors of this Project:

Dr. Roberto G. Valenti 
(Senior Research Scientist,MathWorks Excellence in Innovation Program Lead)

Dr. Bing Li 
(Professor,Clemson University International Center for Automotive Research (CU-ICAR))

## Youtube Video Review
<a href="https://www.youtube.com/watch?v=1A5JWeAHcRw=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="Autonomous Waypoint Navigation" width="240" height="180" border="10" /></a>
 




