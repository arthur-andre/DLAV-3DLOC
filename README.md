# DLAV-3DLOC
Project on 3D vehicle localization for the course Deep Learning for Autonomous Vehicles. 

<a href="https://www.tri.global/" target="_blank">
 <img align="right" src="/media/figs/tri-logo.png" width="20%"/>
</a>

- [Introduction](#introduction)
- [Contribution Overview](#contribution-overview)
- [Dataset details](#dataset-details)
- [Experimental Setup](#dataset-stats)
- [How to use](#how-to-use)
- [Results](#evaluation-metrics)
- [Conclusion](#ipython-notebook)
- [References](#references)


![](media/figs/ddad_viz.gif)

## Introduction

In this project, we aim to train a model to perform 3D car detection from RGB images. The ultimate goal is to integrate this module into other components in order to build an autonomous road planning algorithm.

xxx: gif de notre algo qui fonctionne. 

## Contribution Overview
From the paper "Investigating Localization Errors in Monocular 3D Object Detection," following diagnostic experiments, the research team inferred that the most significant potential for performance enhancement lies within the realms of localization and 3D prediction.

xxx: Incorporate curves with ground truth components.

We aimed to pursue this direction further, exploring multiple possibilities:

Our primary objective involved improving depth prediction, a major challenge faced by 3D detection models without LiDAR. 
In fact, based on the curve in Figure 1, there is a notable potential increase in Average Precision (AP) score from the baseline to achieving perfect depth prediction. 
In "DD3D: Is Pseudo-Lidar essential for Monocular 3D Object Detection?", employing pre-trained models on a large-scale depth LiDAR dataset resulted in enhanced localization performance.
Specifically, we utilized a DLA-34 backbone pretrained through self-supervised learning on the DDAD15 dataset (**https://github.com/TRI-ML/DDAD**). 
Initially, the backbone was pretrained on ImageNet, augmenting the model's classification ability. Our objective is to provide depth mapping to the neck and head of our model.

Our secondary objective focused on enhancing localization prediction. 
Notably, from the curve in xxx, we observed that the largest potential improvement in AP score lies in localization performance.
Upon analyzing our model, we discovered that the 3D loss solely captured its dimensions, without considering factors such as intersection over union (IOU). 
After implementing ourselves a simple IOU, we identified the presence of noise in our loss function and addressed it by introducing a distance notion to attract predicted boxes towards the ground truth boxes.
To ensure well-shaped boxes, we also incorporated an aspect loss along with the IOU loss. 
To gain a better understanding of the impact of each loss function, we plotted loss curves and obtained corresponding scores to demonstrate the utility of each loss.


## Experimental Setup
- First, we tested the baseline model from the paper in order to retrieve the scores on the same validation set.
- Then, we loaded the depth pre-trained weights in the DLA-34 backbone, re-trained on the kitti dataset and observed the results.
- We also implemented the IOU loss and noted that the loss was noisy and was not going down.
- We suggested that adding a distance notion (IOU->DIOU) would add slope to the loss and enhance training.
- We tried to outperform this new DIOU loss by adding an aspect loss, penalising the box dimensions prediction error only if the IOU>0,5. 

## Dataset details
The 3D object detection benchmark consists of 7481 training images and 7518 test images, comprising a total of 80.256 labeled objects. 
Training RGB images are paired with label txt files. A label file is build with multiple lines, that is made following this structure (from kitti [readme](https://github.com/bostondiditeam/kitti/blob/master/resources/devkit_object/readme.txt)): 
|Values  |  Name  |    Description|
|--------|--------|---------------|
|   1    | type   |     Describes the type of object. |
|   1    | truncated |   Float where truncated refers to the object leaving image boundaries. |
|   1    | occluded  |   Integer indicating occlusion state. |
|   1    | alpha     |   Observation angle of object. |
|   4    | bbox      |   2D bounding box of object in the image. |
|   3    | dimensions |  3D object dimensions: height, width, length (in meters). |
|   3    | location   |  3D object location x,y,z in camera coordinates (in meters) |
|   1    | rotation_y |  Rotation ry around Y-axis in camera coordinates. |
|   1    | score      |  Only for results: confidence in detection, needed for p/r curves. |

While the calib folder, contains the calibration of the camera for each RGB image. Since we use left RGB images, we only use the `P2` camera matrix.
From this matrix, can be retrieved the intrinsic and extrinsic parameters of the camera: 

|f_u|f_v|c_u|c_v|t_x|t_y|
|---|---|---|---|---|---|
|P2[0,0]|P2[1,1]|P2[0,2]|P2[1,2]|-P2[0,3]/f_u|-P2[1,3]/f_v|


## How to use
### Environment setup
This repo is tested on our local environment (python=3.7.7, cuda=11.1, pytorch=1.13), and we recommend you to use anaconda to create a virtual environment:
Adapt python version, and pytorch installation version depending on your cuda version. Check with `nvidia-smi`. 

```bash
conda create -n monodle python=3.7.7
```
Then, activate the environment:
```bash
conda activate monodle
```

Install  Install PyTorch (1.10.1 in our case):

```bash
pip install torch==1.10.1+cu111 torchvision==0.11.2+cu111 torchaudio==0.10.1 -f https://download.pytorch.org/whl/cu111/torch_stable.html
```

and other  requirements:
```bash
pip install -r requirements.txt
```

### Dataset Location
Please download [KITTI dataset](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) and organize the data as follows:

```
#ROOT
  |data/
    |KITTI/
      |ImageSets/ [already provided in this repo]
      |object/			
        |training/
          |calib/
          |image_2/
          |label/
        |testing/
          |calib/
          |image_2/
```


## Results

From first contribution, that is using a depth-pre-trained DLA-34 backbone on mass lidar data, we have these results:
(all medium difficulties)
|Scores| imageNet pretrained | DDAD15M pretrained |
|-----|---------------------|--------------------|
|Bbox |        xx           |         xx         |
|BEV  |        xx           |         xx         |
|3D   |        xx           |         xx         |
|AOS  |        xx           |         xx         |

The results obtained from this project are...
Final Results for medium level 3D car detection
| changes | baseline(paper) | baseline | pretraineddepth | IoU | DIoU | CIoU | pretraineddepth+iou |
|---------|-----------------|----------|-----------------|-----|------|------|---------------------|
| scores  | xxx             |   xxx    | xxx             | xxx | xxx  | xx   |   xx                |


## Conclusion

In conclusion, this project...

- Summary of findings
- Future work
- ...

## References

- Reference 1
- Reference 2
- ...
