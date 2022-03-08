
# Dataset preparation

## Retrieve the necessary data from ScanNet

First you need to sign the necessary agreement and obtain the **download-scannet.py** script to download the ScanNet data.
To do so follow the instruction in the original [ScanNet repository](https://github.com/ScanNet/ScanNet).


The necessary data to download is the **scannet_frames_25k.zip** and **Scannet v2** for both the training and validation set
next you should organize your folder structure so that in main folder you have:
```
This Repo
 |
 |--scannet_25_k\
 |  |
 |  |--scene0000_00\
 |  |  |
 |  |  |--color\
 |  |  |  |-- 0000000.jpg
 |  |  |  |-- 0000100.jpg
 |  |  |  |-- ...
 |  |  |-- depth\
 |  |  |  |-- 0000000.jpg
 |  |  |  |-- 0000100.jpg
 |  |  |  |-- ...
 |  |  |-- instance\
 |  |  |  |-- 0000000.jpg
 |  |  |  |-- 0000100.jpg
 |  |  |  |-- ...
 |  |  |-- label\
 |  |  |  |-- 0000000.jpg
 |  |  |  |-- 0000100.jpg
 |  |  |  |-- ...
 |  |  |-- etc
 |  |  |-- etc
 |  |--scene0000_01\
 |  |  |-- color\
 |  |  |-- depth\
 |  |  |-- ...\
 |  ...
 |
 |--scans\
 |  |--scene0000_00\
 |  |  |-- scene0000_00.txt
 |  |  |-- scene0000_00.aggregation.json
 |  |  |-- scene0000_00_vh_clean_2.0.010000.segs.json
 |  |  |-- scene0000_00_vh_clean_2.labels.ply
 |  |  |-- scene0000_00_vh_clean_2.ply
 |  |  
 |  |--scene0000_01\
 |  |  |-- scene0000_01.txt
 |  |  |-- scene0000_01.aggregation.json
 |  |  |-- scene0000_01_vh_clean_2.0.010000.segs.json
 |  |  |-- scene0000_01_vh_clean_2.labels.ply
 |  |  |-- scene0000_01_vh_clean_2.ply

```

## Processing the data

To process the data we will use [ray](https://docs.ray.io/en/latest/index.html) to handle the multiprocessing on multiple clusters. Ray can also be used on single machine. If you have troubles running it, it should be easy to convert the code to use the python standard multiprocessing library.

This processing steps will take some hours to run, please be patient.

### 1) Preparing the annotated ply files

In this step we will create the scene pcd with semantic and instance information (the one provided by scannet do not directly provide the information regarding the instances)

```bash
python 1.created_annotated_ply.py
```


### 2) Creating the point cloud for the partial scenes

```bash
python 2.create_partial_pcd.py
```


### 3) Create the jsons

```bash
python 3.create_partial_jsons
```
