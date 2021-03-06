# **Traffic Sign Classifier** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data distributed.

![bar chart](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/Unknown.png)

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because color is not the key issue for traffic sign classification.

Here is an example of a traffic sign image before and after grayscaling.

![alt text](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/original%26grayscaled.png)

As a last step, I normalized the image data because normalize process change the image value (0~255) to (-1~1) is more easy to apply logistics regression.

I decided to generate additional data because more train data is helped to inhance performance of classification model.

To add more data to the the data set, I used the following techniques because image translation, rotation and resize could help to avoid overfitting.

Here is an example of an original image and an augmented image:

![alt text](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/augmented_image.png)

The difference between the original data set and the augmented data set is that augmented data set is switch from original data by translation, rotation and resize.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 RGB image   							| 
| Convolution 3x3     	| 1x1 stride, VALID padding, outputs 32x32x64 	|
| RELU					|	activation								|
| Max pooling	      	| 2x2 stride,  outputs 14x14x16 				|
| Convolution 3x3	    | 1x1 stride, VALID paddding, outputs 10x10x16 	|
| Pooling		| 2x2 stride,  outputs 5x5x16 								|
|	Flatten		|	outputs 400											|
| Fully connected 	x 3 times			| outputs 120 to 84 to 43 			|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an softmax, logistics and cross-entropy function, and then calculate the training loss, optimizer is Adamoptimizer, because it's fast optimizer than SGD, hyperparameters as below:
EPOCHS = 10
BATCH_SIZE = 126
learning_rate = 0.005

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 126
* validation set accuracy of 0.974 
* test set accuracy of 0.985

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen? ————lenet architecture has been chosen, since this is effective image classifier architecture.
* What were some problems with the initial architecture?————in previous time, training accuracy and validation accuracy is not exceed 90%.
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.————in the first try, i didn't add augmented image, low accuracy on both of training set and validation set, then i generated augmented image by translate, rotate and resize.
* Which parameters were tuned? How were they adjusted and why?———— 
  1:Frist try epochs set as 56, but i found that both training and validation accuracy are not increase after 7 or 8 epochs, so i turn it to 10 epochs. 
  2:BATCH_SIZE has been tuned from 156 to 126, accuracy is not keep pace with it, so keep this value.
  3:Inital learning-rate is 0.05, highest validation accuracy is 92%, tweek it to 0.005, hit 98%.

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:


![speed limit(30km/h)](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/New_Image/0.png) speed 
limit(30km/h)


![go straight or left](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/New_Image/1.png)go straight or left


![ahead only](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/New_Image/2.png)ahead only


![no vehicles](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/New_Image/3.png)no vehicles


![right-of-way at the next intersection](https://github.com/StephenZhang945/P2_Traffic_Sign_Classifier/blob/master/New_Image/4.png)right-of-way at the next intersection

The second image might be difficult to classify because after convert from RGB to grayscale， "go left" signal in this image maybe ignored or confused in different angle of view or shadow.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| speed limit(30km/h)     		| speed limit(30km/h   		 	| 
| go straight or left     		| go straight or left						|
| ahead only					| ahead only						|
| no vehicles  		| no vehicles						|
| right-of-way at the next intersection			| right-of-way at the next intersection 		|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 98%.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 15th cell of the Ipython notebook.

For the second image, the model is relatively sure that this is a "go straight or left" sign (probability of .59), and the image does contain a correct sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .59    | Go straight or left  	| 
| .38    | Priority road					   	|
| .01		 	| Traffic signals		   		|
| .01  		| General caution		   		|
| 0		  	 | Yield.              		|

For the rest of images, the model is give the 100% prediction.

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


