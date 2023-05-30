# DLAV-3DLOC
Project on 3D vehicle localization for the course Deep Learning for Autonomous Vehicles. 


In this project, we aim to train a model to perform 3D car detection from RGB images. The ultimate goal is to integrate this module into other components in order to build an autonomous road planning algorithm.

xxx: gif de notre algo qui fonctionne. 

## Contributions
From the paper "Investigating Localization Errors in Monocular 3D Object Detection," following diagnostic experiments, the research team inferred that the most significant potential for performance enhancement lies within the realms of localization and 3D prediction.

xxx: Incorporate curves with ground truth components.

We aimed to pursue this direction further, exploring multiple possibilities:

Our primary objective involved improving depth prediction, a major challenge faced by 3D detection models without LiDAR. Furthermore, based on the curve in Figure 1, there is a notable potential increase in Average Precision (AP) score from the baseline to achieving perfect depth prediction. In "DD3D: Is Pseudo-Lidar essential for Monocular 3D Object Detection?", employing pre-trained models on a large-scale depth LiDAR dataset resulted in enhanced localization performance (xxx provide more details). Specifically, we utilized a DLA-34 backbone pretrained through self-supervised learning on the DDAD15 dataset (**https://github.com/TRI-ML/DDAD**). Initially, the backbone was pretrained on ImageNet, augmenting the model's classification ability. Our objective is to provide depth mapping to the neck and head of our model.

Our secondary objective focused on enhancing localization prediction. Notably, from the curve in xxx, we observed that the largest potential improvement in AP score lies in localization performance. Upon analyzing our model, we discovered that the 3D loss solely captured its dimensions, without considering factors such as intersection over union (IOU). After implementing ourselves a simple IOU, we identified the presence of noise in our loss function and addressed it by introducing a distance notion to attract predicted boxes towards the ground truth boxes. To ensure well-shaped boxes, we also incorporated an aspect loss along with the IOU loss. To gain a better understanding of the impact of each loss function, we plotted loss curves and obtained corresponding scores to demonstrate the utility of each loss.

## Experimental Setup

### Requirements

To run this project, you will need the following dependencies:

- Dependency 1
- Dependency 2
- ...

### Installation

To install the project dependencies, follow these steps:

1. Step 1
2. Step 2
3. ...

## Dataset Description

The dataset used in this project is...

- Description 1
- Description 2
- ...

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
