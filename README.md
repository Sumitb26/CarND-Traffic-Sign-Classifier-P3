# **Traffic Sign Recognition** 


**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./dataset_visualize.png "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./test_images/2.jpg "Traffic Sign 1"
[image5]: ./test_images/13.jpg "Traffic Sign 2"
[image6]: ./test_images/17.jpg "Traffic Sign 3"
[image7]: ./test_images/25.jpg "Traffic Sign 4"
[image8]: ./test_images/27.jpg "Traffic Sign 5"

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data is distributed among 43 classes of traffic signs.

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because LeNet architecture required one channel images.

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image2]

As a last step, I normalized the image data so that the pixels have similar distribution which makes covergence faster while training the network.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 3x3     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, valid padding, outputs 14x14x6	|
| Convolution 3x3	    | 1x1 stride, valid padding, outputs 10x10x16	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, valid padding, outputs 5x5x16	    |
| Flatten				| outputs 400              						|
| Dropout   	      	| rate 0.5              	                    |
| Fully connected		| outputs 120            						|
| Relu  				|                         						|
| Dropout   	      	| rate 0.5              	                    |
| Fully connected		| outputs 84            						|
| Relu  				|                         						|
| Dropout   	      	| rate 0.5              	                    |
| Fully connected		| outputs 43            						|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an Adam optimizer with learning rate of 0.0006. I trained for 150 epochs with batch size of 128.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 99.6%
* validation set accuracy of 97%
* test set accuracy of 95.1%

* First I choose LeNet-5 architecture as it worked well on MNIST dataset.
* The model didn't work as the input images were not preprocessed according to LeNet requirements.
* After preprocessing LeNet architecture was adjusted to generate output for 43 classes.
* This led to generalization gap i.e overfitting as validation accuracy didnt increase as training accuracy.
* Added dropout layer with rate = 0.5 to avoid overfitting and allow model to generalize better on unseen data.
* Learning rate was tuned according to convergence of loss function and the batch_size was adjusted in order to reach required accuracy.
* Convolution layers was chosen to allow model to learn features from image dataset. Dropout was useful in making this model a success by allowing more generalization.


### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

The first image might be difficult to classify because it's tilted view.
The second image is quite easy to classify as it is clear and straight.
The third and forth image have a lot of marks on the sign and may make it difficult to classify.
The fifth image looks a lot similar to other signs example "right turn" when considering grayscale and normalized image.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Road work      		| Road work   									| 
| No entry     			| No entry 										|
| Speed limit (50km/h)	| Speed limit (50km/h)   						|
| Yield 	      		| Yield        					 				|
| Pedestrians			| Keep right          							|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This compares favorably to the accuracy on the test set of 95.1%.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a road work sign (probability of 0.99), and the image does contain a road work sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .9924        			| Road work   									| 
| .0057     			| Wild animals crossing							|
| .0013					| Bicycles crossing								|
| .0003	      			| Double curve					 				|
| .0002				    | Dangerous curve to the right					|


For the second image, the model is relatively sure that this is a no entry sign (probability of 1), and the image does contain a no entry sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.0        			| No entry   									| 
| 0     		      	| Turn left ahead      							|
| 0				     	| Stop             								|
| 0	      		    	| Keep right					 				|
| 0 				    | Roundabout mandatory      					|

For the third image, the model is relatively sure that this is a Speed limit (50km/h) sign (probability of 0.93), and the image does contain a Speed limit (50km/h) sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .93        			| Speed limit (50km/h)							| 
| .03     			    | Speed limit (30km/h)							|
| .007					| No vehicles    								|
| .006	      			| Speed limit (80km/h)			 				|
| .0057				    | Keep right                     				|

For the forth image, the model is relatively sure that this is a yield sign (probability of 1.0), and the image does contain a yield sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.0        			| Yield        									| 
| 0     	       		| Priority road       							|
| 0		       			| Keep right     								|
| 0	         			| Ahead only					 				|
| 0 				    | Speed limit (50km/h)      					|

For the fifth image, the model is not sure that this is a pedestrian sign (probability of 0), and the image does contain a keep right sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .37        			| Keep right   									| 
| .11        			| Turn left ahead   							|
| .05					| Go straight or right 							|
| .05	      			| No entry   					 				|
| .05				    | Yield                        					|



