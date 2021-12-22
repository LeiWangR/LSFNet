# A Feature Dataset for Scene Understanding and its Feature Analysis

*The author performed the work while he was a Computer Vision Research Intern at iCetana Pty Ltd.*

## 1 Introduction

This repo contains:

- a feature dataset for video classification, including dense trajectory (DT) features extracted from a subset of iCetanaPrivateDataset,
- jupyter notebooks for a simple analysis of the DT features,
- python codes for fisher vector encoding and 
- a jupyter notebook for the use of fisher score in feature selection.

This repo is for the ICIP2019 paper:

Lei Wang, Du Q. Huynh, and Moussa Reda Mansour, "**Loss Switching Fusion with Similarity Search for Video Classification**," *2019 IEEE International Conference on Image Processing (ICIP)*, 2019, pp. 974-978, doi: 10.1109/ICIP.2019.8803051. [[ArXiv]](https://arxiv.org/abs/1906.11465)[[BibTex]](#citation)

## 2 Dataset

we propose a novel video classification system that would benefit the scene understanding task. We define our classification problem as classifying
background and foreground motions using the same feature representation for outdoor scenes. More detailed information can be found in our paper.

### 2.1 Feature dataset

The subset of iCetanaPrivateDataset contains around 270 videos of various lengths. The average length of the videos in this dataset is approx. 280 frames, with long videos up to 19645 frames. They were captured in outdoor environments so issues, such as tree waving, camera shaking, noise, illumination changes, and rain, are common. Some videos have human motion also. The outdoor scenes include car parks, train stations, bus stops, etc. This subset has been manually labelled with 6 background motion class labels: tree waving, camera shaking, noisy video, rainy, illumination, and normal video:

- Illumination: this class cover all the videos that has light changes as well as different illumination conditions
- Noise: this class covers the videos that are captured by noise sensor, some noise may cause by environment variations
- Normal: this class covers all the normal videos, some may contain less noise but may not affect the performance of video processing
- Rain: this class covers all the videos which has the noise caused by raining, currently this class only has 3 videos
- Shake: this class contains all the noise videos that are caused by the camera shaking
- Wind: this class covers the dynamic background, and currently most of them are the tree waving problems.

There are 3 foreground human motion class labels: general body movements, human-object interaction, and human-human interaction. Videos having both background and foreground motions have two class labels. In this paper, the 3 types of foreground motion are grouped together into one class.

We have provided the DT features extracted from this dataset in this repo, and features include:

- HOG
- HOF
- MBH (MBHx and MBHy)
- trajectory
- DT features/[fisher vectors](https://drive.google.com/file/d/1NWikCxiBjX1s6Khp9X9ue20mtv17ApdT/view?usp=sharing)

We also provide the features extracted from C3D FC6 and FC7 (after dropout) layers in this repo.

The labels are provided in csv file in this repo:

- `all_labels.csv`: 6 background motion classes (start from 0 to 5)
- `human_labels.csv`: with/without human motions (with human motions are labelled as 1)


### 2.2 Evaluation protocols

There are two evaluation protocols for this feature dataset:

- testing how well the 6 background motion classes are classified. This is a multi-class classification problem;
- testing how well the foreground motion is separated from those background motions. This is a binary classification problem.

## 3 Results of LSFNet

Note that the results shown in the following table are for the whole dataset presented in the paper. 

| Algorithms  | Background env. motion | Foreground human motion | 
| ------------- | :---: | :---: |
|  Fisher score + CCA |  81.5 |  85.2 |
|  DT + FV + Fisher score + LSH |  83.6 | 86.5  |
|  LSFNet | 83.3  |  85.2 |
|  LSFNet + Fisher score |  85.2 |  87.0 |
|  Our whole system | 88.9  |  90.7 |


## 4 Citations
<a name="citation"></a>
You can cite the following paper for the use of this repo:

```
@INPROCEEDINGS{lei_icip_2019,
  author={Wang, Lei and Huynh, Du Q. and Mansour, Moussa Reda},
  booktitle={IEEE ICIP}, 
  title={Loss Switching Fusion with Similarity Search for Video Classification}, 
  year={2019},
  volume={},
  number={},
  pages={974-978},
  doi={10.1109/ICIP.2019.8803051}}

```
