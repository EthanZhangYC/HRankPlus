# An extension version of our CVPR 2020, oral: HRank: Filter Pruning using High-Rank Feature Map ([Link](https://128.84.21.199/abs/2002.10179)).

### We are now releasing this code under the request of many friends. However, we are not sure if this code is stable. Please contact us if you have found any problem, which would be appreciated.

### In the next two or three months, we will continue to maintain this repository and the pruned models will be released constantly. 

## Tips

Any problem, please contact the authors via emails: lmbxmu@stu.xmu.edu.cn or ethan.zhangyc@gmail.com, or adding the first author's wechat as friends (id: lmbcxy if you are using wechat) for convenient communications. Do not post issues with github as much as possible, just in case that I could not receive the emails from github thus ignore the posted issues.


## Citation
If you find HRank useful in your research, please consider citing:

```
@inproceedings{lin2020hrank,   
  title     = {HRank: Filter Pruning using High-Rank Feature Map},
  author    = {Lin, Mingbao and Ji, Rongrong and Wang, Yan and Zhang, Yichen and Zhang, Baochang and Tian, Yonghong and Ling, Shao},
  booktitle = {Computer Vision and Pattern Recognition (CVPR)},
  year      = {2020}
}
```

## Running Code

In this code, you can run our models on CIFAR-10 and ImageNet dataset. 

For rank generation, the code has been tested by Python 3.6, Pytorch 1.0 and CUDA 9.0 on Ubuntu 16.04. And for evluating(fine-tuning), we recommend you to run with PyTorch 0.4 for the usage of Thop.


### Rank Generation

```shell
python rank_generation.py \
--dataset [dataset name] \
--data_dir [dataset dir] \
--pretrain_dir [pre-trained model dir] \
--arch [model arch name] \
--limit [batch numbers] \
--gpu [gpu_id]

```
For the ease of reproducibility, we provide the extracted ranks [here](https://drive.google.com/drive/folders/1kwOFEtmUw6jwk_qNpLydwUjlouuexd5R?usp=sharing):


### Model Training

##### 1. CIFAR-10

```shell
CUDA_VISIBLE_DEVICES=[gpu_id] \
python evaluate_cifar.py \
--data_dir [CIFAR-10 dataset dir] \
--job_dir ./result/[model name]/[folder name] \
--arch [model name](vgg_16_bn, resnet_56, resnet_110, googlenet, densenet_40) \
--use_pretrain \
--pretrain_dir [pre-trained model dir] \
--compress_rate [compress rate]
```

##### 2. ImageNet

```shell
CUDA_VISIBLE_DEVICES=[gpu_id] \
python evaluate.py \
--data_dir [ImageNet dataset dir] \
--job_dir ./result/[model name]/[folder name] \
--arch [model name](resnet_50, mobilenet_v1, mobilenet_v2) \
--use_pretrain \
--pretrain_dir [pre-trained model dir] \
--compress_rate [compress rate]
```

The following are the examples of compression rate setting for several models: 
(Please note that the following compression rates are only used to demonstrate the parameter format, which may not be used in our experiment)

|  Model      | Compress Rate |
|:-------------:|:-------------------------:|
| VGG-16-BN | [0.45]\*7+[0.78]\*5 | 
| ResNet-56 | [0.]+[0.18]\*29 | 
| ResNet-110 | [0.]+[0.2]\*2+[0.3]\*18+[0.35]\*36 | 
| GoogLeNet | [0.3]+[0.6]\*2+[0.7]\*5+[0.8]\*2 | 
| DenseNet-40 | [0.]+[0.4]\*12+[0.2]+[0.5]\*12+[0.3]+[0.6]\*12 | 
| ResNet-50 | [0.1]+[0.2]\*3+[0.5]\*16 | 
| MobileNet-V1 | [0.]+[0.3]\*12 | 
| MobileNet-V2 | [0.]+[0.3]*7 | 

After training, totally four files can be found in the `job_dir`, including best model, final model, config file and logger file.

## Pre-trained Models 

Additionally, we provide the pre-trained models used in our experiments. 


### CIFAR-10:
 [Vgg-16](https://drive.google.com/open?id=1i3ifLh70y1nb8d4mazNzyC4I27jQcHrE) 
| [ResNet56](https://drive.google.com/open?id=1f1iSGvYFjSKIvzTko4fXFCbS-8dw556T) 
| [ResNet110](https://drive.google.com/open?id=1uENM3S5D_IKvXB26b1BFwMzUpkOoA26m) 
| [DenseNet-40](https://drive.google.com/open?id=12rInJ0YpGwZd_k76jctQwrfzPubsfrZH) 
| [GoogLeNet](https://drive.google.com/open?id=1rYMazSyMbWwkCGCLvofNKwl58W6mmg5c) 

### ImageNet:
 [ResNet50](https://drive.google.com/open?id=1OYpVB84BMU0y-KU7PdEPhbHwODmFvPbB)
