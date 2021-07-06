# lidar_imu_calib

### overview

when develop slam based on 3D lidar, we often use imu to provide priori for matching algorithm(icp, ndt), so the transform between lidar and imu need to be calibrated.For matching algorithm, attitude in transfom is more important than position in transform, and position often be set to 0. So this repo concentrate on calibrate attitude component in transform between lidar and imu.

### prerequisite

- [ROS](http://wiki.ros.org/kinetic/Installation/Ubuntu)
- [ndt_omp](https://github.com/koide3/ndt_omp)
### install ndt_omp to system catalog
```
git clone https://github.com/BohemianRhapsodyz/lidar_imu_calib.git
cd ndt_omp
mkdir build
cd build
cmake ..
make
sudo make install
```
### step

1. use rosbag tool record imu and lidar data

   ```
   rosbag record /imu /lidar_points
   ```

2. config launch file

   ```
   lidar_topic: your lidar topic
   imu_topic: ypur imu topic
   bag_file: your bag 
   ```


3. start

   ```
   roslaunch lidar_imu_calib calib_exR_lidar2imu.launch
   ```
### note

- Replace your bag path in calib_exR_lidar2imu.launch
- This Initial alignment function in this tool is used for high precision IMU(FOG), requiring static for 60s. For mems grade IMU, just use the orientation quat provided by AHRS algorithm.  

