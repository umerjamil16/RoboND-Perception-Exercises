# Object Recognition with Python, ROS and PCL

In this exercise, I built a perception pipeline in ROS with a very simple gazebo world, where color and shape features (from the table top objects) which can be extracted in order to train a classifier to detect them.


## Setup

* Make sure you have all the dependencies resolved by using the `rosdep install` tool and running `catkin_make`:  
 
```sh
$ cd ~/catkin_ws
$ rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
$ catkin_make
```

* If it's not already there, add the following lines to your `.bashrc` file  

```
export GAZEBO_MODEL_PATH=~/catkin_ws/src/sensor_stick/models
source ~/catkin_ws/devel/setup.bash
```

## Preparing for training

Launch the `training.launch` file to bring up the Gazebo environment: 

```sh
$ roslaunch sensor_stick training.launch
```
You should see an empty scene in Gazebo with only the sensor stick robot.

## Capturing Features
Next, in a new terminal, run the `capture_features.py` script to capture and save features for each of the objects in the environment.  This script spawns each object in random orientations (default 5 orientations per object) and computes features based on the point clouds resulting from each of the random orientations.

```sh
$ rosrun sensor_stick capture_features.py
```

The features will now be captured. It should take 5-10 sec. for each random orientations (depending on your machine's resources) so with 7 objects total it takes awhile to complete. When it finishes running you should have a `training_set.sav` file.

## Training

Once the feature extraction has successfully completed, model can be trained. Please note that the `sklearn` and `scipy` Python packages are required.  The can be installed using `pip`:

```sh
pip install sklearn scipy
```

After that, all we need to do is to run the `train_svm.py` model to train an SVM classifier on the labeled set of features.

```sh
$ rosrun sensor_stick train_svm.py
```

## Classifying Segmented Objects

If everything went well, we now have a trained classifier and we're ready to do object recognition!  