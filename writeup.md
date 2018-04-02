### Project Writeup

Once you have completed the code implementation, document your results in a project writeup using this [template](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/writeup_template.md) as a guide. The writeup can be in a markdown or pdf file. 

[image1]: ./bar.jpg "Visualization"

[image_before]: ./before.jpg  "Before preprocessing"
[image_after]: ./after.jpg  "Before preprocessing"

[test]: ./test.jpg 



### Data Set Summary & Exploration

#### 1. Basic summary of the data set

I used numpy and matplotlib libraries to get summary of the data set provided.
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Exploratory visualization of the dataset

Here is an exploratory visualization of the data set. It is a bar chart showing number of images in each class of trafic sign.
If the number of images in a particular class is high then test accuracy for particular class will be high.

![alt text][image1]


### Design and Test a Model Architecture

#### Preprocessing of data

Function preProcessData takes image dataset as input. Since our neural network takes single channel image as input, we need to convert 3 channel input image to single channel image.
Below steps are followed to do so
1. taking average of all 3 channel values to convert to single channel.
2. Normalizing value of each pixel in range of -1 to 1. ((pixel-128)/128)
3. Since depth(channel) of image is lost so need to reshape input data.


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

#### 3. how I trained my model

To train the model i used AdamOptimizer as optimizer and below parameters
Batch size = 128
Number of epochs = 100
Initial learning rate = 0.001

#### 4. Approch taken and accuracy

My final model results were:
* training set accuracy of 99.5% 
* validation set accuracy of 96% 
* test set accuracy of 94.3% 

* I choose Lenet architecture for classification.
* Because It takes 32x32 image size as input which is same as images provided in input set.
* Observing result accuracy above model is identifying almost 95% traffic signs.


### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are 10 German traffic signs that I found on the web:

![alt text][test] 

Images with sign "80 km/h", "50 km/h", "Road work" might be difficult to classify because in those images traffic signs are looking streched towards an angle because images are captured at different angles.



#### 2. Prediction of model

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Stop Sign      		| Stop sign   									| 
| No entry     			| No entry 										|
| 50 km/h				| 30 km/h										|
| Bumpy road    		| Traffic signals					 			|
| Road work		        | Road work	    							    |
| Bicycles crossing     | Children crossing   							| 
| Turn left ahead    	| Turn left ahead								|
| Ahead only			| Ahead only									|
| 80 km/h        		| Vehicles over 3.5 metric tons prohibited		|
| No passing	        | No passing     							    |


#### 3. softmax probabilities for each prediction

* 1st image : the model is relatively sure that this is a stop sign (probability of 0.99), and the image does contain a stop sign. The top five soft max probabilities were [9.99983311e-01, 9.11827556e-06, 5.97807548e-06, 7.92422156e-07, 6.28333510e-07] which corresponds to array of class label [14,  4, 13, 15, 12]

* 2nd image : the model is 100% sure that sign is No entry (probability of 1.00), and the image does contain a No entry sign. The top five soft max probabilities were [1.00000000e+00, 0.00000000e+00, 0.00000000e+00, 0.00000000e+00, 0.00000000e+00] which corresponds to array of class label [17,  0,  1,  2,  3]
        
* 3rd image : the model is 100% sure that sign is speed limit 30 km/h  (probability of 1.0), but the image does not contain a speed limit 30 km/h sign. The top five soft max probabilities were [1.00000000e+00, 6.01118305e-29, 4.55140306e-35, 0.00000000e+00, 0.00000000e+00] which corresponds to array of class label [ 1,  0, 40,  2,  3]. Reason why it is not able to detect is sign is bit tilted to one side. 
  
* 4th image : the model is 99% sure that sign is bumpy road (probability of 0.99), but the image does not contain abumpy road sign. The top five soft max probabilities were [9.99974608e-01, 2.51842139e-05, 1.36329390e-07, 2.21694112e-08, 2.68354904e-11] which corresponds to array of class label [26, 22, 18, 25, 29] 

* 5th image : the model is 100% sure that this is a Road work sign (probability of 1.0), and the image does contain a Road work sign. The top five soft max probabilities were [1.00000000e+00, 5.69664162e-13, 1.48233713e-14, 2.21488464e-15,
        1.14142984e-16] which corresponds to array of class label [25, 20, 30, 22, 26]
        
* 6th image : the model is 96% sure that this is a Bicycles crossing sign (probability of .96), but the image does not contain a Bicycles crossing sign. The top five soft max probabilities were [9.65143442e-01, 3.23487818e-02, 2.48215161e-03, 1.03619195e-05, 9.34415129e-06] which corresponds to array of class label [28, 23, 20, 35, 19] . Reason why it is not able to detect is sign is bit tilted to one side.

* 7th image : the model is relatively sure that this is a Turn left ahead sign(probability of 0.99), and the image does contain a Turn left ahead sign. The top five soft max probabilities were [9.94352698e-01, 4.48922860e-03, 1.03775563e-03, 7.72533458e-05, 3.04797686e-05] which corresponds to array of class label [34,  8, 26, 35, 28]
        
* 8th image : the model is 100% sure that this is a Ahead only sign (probability of 1.0), and the image does contain a Ahead onlysign. The top five soft max probabilities were [1.00000000e+00, 4.51906139e-08, 3.96778432e-08, 3.02399261e-09, 7.47845327e-11] which corresponds to array of class label [35, 36, 13, 25, 20] 

* 9th image : the model is 99% sure that this is a 80 km/h sign (probability of .99), but the image does not contain a 80 km/h  sign. The top five soft max probabilities were [9.98707652e-01, 1.10457640e-03, 1.85043391e-04, 2.72662828e-06, 1.25558147e-10] which corresponds to array of class label [16,  3, 11,  5, 42] . Reason why it is not able to detect is sign is bit tilted to one side.

* 10th image : the model is 100% sure that this is a Ahead only sign (probability of .99), and the image does contain a Ahead onlysign. The top five soft max probabilities were [9.99918580e-01, 5.82226930e-05, 2.32605216e-05, 1.20974901e-08, 1.31041467e-09] which corresponds to array of class label [ 9, 41, 17, 10, 20]         
        
