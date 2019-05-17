
# Euclidean Clustering with ROS and PCL

Here, in this module, I built a basic perception pipeline in ROS and PCL.

The gazebo world contains a table and  some random objects.

A simple stick robot with an RGB-D camera attached to its head via a pan-tilt joint is placed in front of the table. 

Here's a brief summary of how to run this module:

1. First of all copy/move the `sensor_stick` package to `/src` directory of your active ros workspace. 

2. Make sure you have all the dependencies resolved by using the rosdep install tool and run `catkin_make`:  

```sh
$ cd ~/catkin_ws
$ rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
$ catkin_make
```
3. Add following to your .bashrc file
```
export GAZEBO_MODEL_PATH=~/catkin_ws/src/sensor_stick/models

source ~/catkin_ws/devel/setup.bash
```

4. Test the simulation setup by launching the gazebo environment. The command stated below will open a gazebo world along with an rviz window. 

```sh
$ roslaunch sensor_stick robot_spawn.launch
```
![screen shot 2017-07-05 at 12 56 36 pm](https://user-images.githubusercontent.com/20687560/27895526-30da599c-61c8-11e7-80ab-4b4224cfbb10.png)


To build the perception pipeline, I performed the following steps:

2. Created a python ros node that subscribes to `/sensor_stick/point_cloud` topic. 

3. Applied various filters and segment the table using RANSAC. 

4. Created publishers and topics to publish the segmented table and tabletop objects as separate point clouds 

5. Applied Euclidean clustering on the table-top objects (after table segmentation is successful)

6. Create a XYZRGB point cloud such that each cluster obtained from the previous step has its own unique color.

7. Finally the colored cluster cloud is published on a separate topic 
![clusters](https://user-images.githubusercontent.com/9555001/27804180-604d6e04-5fe2-11e7-9f33-d8d8da9a8bc0.png)
