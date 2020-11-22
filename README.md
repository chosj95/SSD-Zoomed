# SSD-Zoomed

## Installation
- Install [PyTorch](http://pytorch.org/) by selecting your environment on the website and running the appropriate command.

- Clone this repository.

- Then download the dataset by following the [instructions](#datasets) below.



## Datasets

Currently, we only provide PFPNet of Pascal VOC version. 

### VOC Dataset

PASCAL VOC: Visual Object Classes

##### Download VOC2007 trainval & test

```
# specify a directory for dataset to be downloaded into, else default is ~/data/
sh data/scripts/VOC2007.sh # <directory>
```

##### Download VOC2012 trainval

```
# specify a directory for dataset to be downloaded into, else default is ~/data/
sh data/scripts/VOC2012.sh # <directory>
```



## Training

- First download the fc-reduced [VGG-16](https://arxiv.org/abs/1409.1556) PyTorch base network weights at: https://s3.amazonaws.com/amdegroot-models/vgg16_reducedfc.pth
- By default, we assume you have downloaded the file in the `SSD-Zoomed/weights` dir:

```
mkdir weights
cd weights
wget https://s3.amazonaws.com/amdegroot-models/vgg16_reducedfc.pth
```

- Use the  following script below to train network .

```
python train.py --dataset 'VOC' --save_folder 'weights/' --basenet './weights/vgg16_reducedfc.pth'
```

- Note:
  - For training, an NVIDIA GPU is strongly recommended for speed.
  - You can pick-up training from a checkpoint by specifying the path as one of the training parameters (again, see `train.py` for options)

**Note**: COCO version and SSD512 are unavailable.

## Evaluation

To evaluate a trained network:

```
python eval.py --save_folder 'weights/' --trained_model 'weights/VOC.pkl'
```



## Performance

VOC2007

mAP

| Model | Scale set | mAP |
| :-----: | :-----------: | --------------- |
| SSD | - | 77.2 |
| Proposed | {1.4, 1.2, 0.8, 0.6} | 77.4 |
| - | {1.2, 1.1, 0.9, 0.8} | 77.6 |
| - | {1.3, 1.2, 1.1, 0.7} | 77.7 |
| - | {1.3, 0.9, 0.8, 0.7} | 77.7 |
| - | {1.3, 1.1, 0.9, 0.7} | 78.0 |

SSD-Zoomed: https://drive.google.com/file/d/1immZILO3aQVaMqvlsivyCj71lSbuBrlw/view?usp=sharing

## References

- A list of other great SSD ports that were sources of inspiration:
  - [amdegroot/ssd.pytorch](https://github.com/amdegroot/ssd.pytorch)
  - [lzx1413/PytorchSSD](https://github.com/lzx1413/PytorchSSD)

