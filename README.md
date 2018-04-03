# Self-Driving-CarND-Traffic-Sign-Classifier
> Please refer to: Self-Driving Car Engineer Nanodegree - Udacity, [Term 1 - Project 2](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project)

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Overview

This project uses a deep convolutional neural network to classify traffic signs. Lenet is used as model.
The CNN model takes as input the [German Traffic Sign Dataset](https://s3.amazonaws.com/video.udacity-data.com/topher/2017/February/5898cd6f_traffic-signs-data/traffic-signs-data.zip) and understands road signs from images. Find another [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset) that can be used.

Goto [notebook](Traffic_Sign_Classifier.ipynb) which shows the code as well full results. The notebook also consist result on on images in folder [new_images](/new_images)

## Prerequisites
To run this project, you need [Miniconda](https://conda.io/miniconda.html) installed(Follow [instructions](https://conda.io/docs/install/quick.html) to quickly install)

## Installation
To create an environment for this project use the following command:
```
conda env create -f environment.yml
```
After the environment is created, it needs to be activated with the command:
```
source activate carnd-term1
```
and open the project's notebook P1.ipynb inside jupyter notebook:
```
jupyter notebook P1.ipynb
```

### Data Set Summary & Exploration

#### 1. Basic summary of the data set

I used numpy and matplotlib libraries to get summary of the data set provided.
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Final model architecture

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Grayscale image    				    | 
| Convolution 5x5     	| 1x1 stride, Valid padding, outputs 28x28x6 	|
| RELU					| Activation function							|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6  				|
| Convolution 3x3	    | etc.      									|
| RELU					| Activation function							|
| Flatten Input         | output    1x400                               |
| Fully connected       | input 1x400 output 120                        |
| RELU                  | Avtivation function                           |
| Drop Out              | keep_prob=0.8                                 |
| Fully connected       | input 1x120 output 84                         |
| Max pooling           | 2x2 stride,  outputs 5x5x16                   |
| RELU                  | Avtivation function                           |
| Drop Out              | keep_prob=0.6                                 |
| Softmax               | Probabilistic Distribution                    |
|						|												|

My final model results were:
* training set accuracy of 99.5% 
* validation set accuracy of 96% 
* test set accuracy of 94.3% 

For prediction result analysis on images downloaded from net visit [writeup.md](/writeup.md).


