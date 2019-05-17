# Tabletop Segmentation
![screen shot 2017-07-05 at 10 49 11 am](https://user-images.githubusercontent.com/20687560/27878614-aff58b20-6173-11e7-909d-41d5d21a23d6.png)
In this exercise, I applied filtering techniques and used RANSAC plane fitting to segment the table in point cloud.  


In brief, following steps were performed:

1. Downsampled the point cloud by applying a Voxel Grid Filter.
2. Applied a Pass Through Filter to isolate the table and objects.
3. Performed RANSAC plane fitting to identify the table.
4. Used the ExtractIndices Filter to create new point clouds containing the table and objects separately.

### To view a .pcd file:

```
$ pcl_viewer filename.pcd 
```
