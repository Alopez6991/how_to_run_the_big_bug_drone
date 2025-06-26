# Quick steps
* ```roscore```
* ``` roslaunch vicon_bridge vicon.launch```
* ``` rosrun vicon_bridge transfer.py```
* ```camera_clean``` or ```clean_camera```
* ```rosrun trisonica trisonica_body_level.py```
* ```roslaunch vrpn_mavros test.launch```
* ```rosbag record - o <name of bag> /topic1 /topic2 ...```
* ```rosrun plotjuggler plotjuggler```
* ```cd /Downloads```
* ```./QGroundControl.AppImage```

# Steps for running Big Bug
## Basic setup
* ```roslaunch vrpn_mavros test.launch```
* ```roslaunch position_to_velocity basic.launch```

## Trajectory flights
* ```roslaunch trajectory_gen constant_vel_launch.launch```
* **Note:** that the trajectory that will run in based on the csv in trajectory_gen/trajectories/csv_trajectories.yaml
  * I sugest using file ```linear_trajectory_constant_heading_edege_only_02.csv``` replace the active file in csv_trajectories.yaml
 
## Trisonica
* make sure the sensor is on. it has a physical on off switch.
* ```rosrun trisonics trisonica_body_level.py```

## realsene 60 Hz
* ```roslaunch realsense2_camera rs_camera.launch align_depth:=true depth_width:=640 depth_height:=480 depth_fps:=30 color_width:=640 color_height:=480 color_fps:=60```

## realsene 100 Hz
* ```roslaunch realsense2_camera rs_camera.launch align_depth:=true depth_width:=640 depth_height:=480 depth_fps:=30 color_width:=640 color_height:=480 color_fps:=100```

## Opticflow
* ```rosrun optic_flow_example optic_flow_lucas_kanade.py --topic='/camera/color/image_raw'```

## data collection (replace linear with your file name)
* ``` rosbag record -o linear /trisonica /trisonica_body_level /trisonica_global /mavros/local_position/pose /mavros/rc/in /mavros/rc/out /mavros/imu/data /mavros/imu/data_raw /camera/color/image_raw```

# Post process
* ``` rosbag play linear.bag```
* 
