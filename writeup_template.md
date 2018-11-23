# **Behavioral Cloning**


**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report



## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* CarND-BehavioralCloning-P4.ipynb notebook contains a well documented code on how the model was obtained and the architecture for the NN used.
* CarND-BehavioralCloning-P4.html is the html version of the notebook.
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* writeup_report.md or writeup_report.pdf summarizing the results
* run1.mp4 video of the car passing the first track. It exists in the output video directory


#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works. The notebook CarND-BehavioralCloning-P4 also contain well documented code
for how the neural network was trained, how the data was collected and preprocessed. I didn't use generator functions as the data was doing well on my
pc in training and the data was enough for moving the car around the first track.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

The first two steps are for data preprocessing, then, I trained the network.

#### The network consists of :
1. Normalization layer
2. Cropping layer. Crop the images from the upper and lower part of the images to help the model train faster
3. Convolution layer -with filter size = 32- followed by a relu activation
4. Max pooling layer with filter size of 2x2.
5. Convolution layer -with filter size = 48- followed by a relu activation
6. Max pooling layer with filter size of 2x2.
7. Convolution layer -with filter size = 64- followed by a relu activation
8. Max pooling layer with filter size of 2x2.
9. flatten the array to 1-D array to process it with a fully connected network.
10. hidden layer with 128 hidden neuron followed by a relu activation and dropout with keep_prob = 50%.
11. hidden layer with 64 hidden neuron followed by a relu activation and dropout with keep_prob = 50%.
12. hidden layer with 32 hidden neuron followed by a relu activation and dropout with keep_prob = 50%.
13. the output neuron for the steering angle.

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting .

The model was trained and validated on different data sets to ensure that the model was not overfitting. It was also trained on a reasonable amount of data to reduce overfitting. The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually.

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road from both clock and counter clock wise driving.

For details about how I created the training data, see the next section.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to try and collect general data by driving both ways and recovering from road sides
to give the neural network most of the cases.

I collected two laps on the first track and a recovery from the sides lap.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting so i reduced the network size and it worked. I also visualised the errors to make sure it was not overfitting nor underfitting.


The final step was to run the simulator to see how well the car was driving around track one. and i tuned the network size and the correction factor
for the right and left camera.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture consisted of a :
1. Normalization layer
2. Cropping layer. Crop the images from the upper and lower part of the images to help the model train faster
3. Convolution layer -with filter size = 32- followed by a relu activation
4. Max pooling layer with filter size of 2x2.
5. Convolution layer -with filter size = 48- followed by a relu activation
6. Max pooling layer with filter size of 2x2.
7. Convolution layer -with filter size = 64- followed by a relu activation
8. Max pooling layer with filter size of 2x2.
9. flatten the array to 1-D array to process it with a fully connected network.
10. hidden layer with 128 hidden neuron followed by a relu activation and dropout with keep_prob = 50%.
11. hidden layer with 64 hidden neuron followed by a relu activation and dropout with keep_prob = 50%.
12. hidden layer with 32 hidden neuron followed by a relu activation and dropout with keep_prob = 50%.
13. the output neuron for the steering angle.


#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][https://github.com/Mahmoud-Selim/CarND-Behavioral-Cloning-P3/blob/master/Screenshots/center_2018_11_22_00_46_25_694.jpg]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to .... These images show what a recovery looks like starting from ... :

![alt text][https://github.com/Mahmoud-Selim/CarND-Behavioral-Cloning-P3/blob/master/Screenshots/center_2018_11_22_00_54_56_040.jpg]
![alt text][https://github.com/Mahmoud-Selim/CarND-Behavioral-Cloning-P3/blob/master/Screenshots/center_2018_11_22_00_55_16_196.jpg]


Then I repeated this process driving backwards on track one. I also tried training over track two and the car drove about half the road but didn't complete so i removed the data as it didn't affect track one.



After the collection process, I had 10,080 number of data points. I then preprocessed this data by normalizing the data to have zero mean and
1 standard deviation. I also cropped the upper side of the images as i thought it ould be distracting for the model.


I finally randomly shuffled the data set and put Y% of the data into a validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was 5 as the error didn't decrease much below it ... I used an adam optimizer so that manually training the learning rate wasn't necessary.

Finally, i plotted the validation and training error as shown below

![alt text][https://github.com/Mahmoud-Selim/CarND-Behavioral-Cloning-P3/blob/master/Screenshots/trainVSvalid_error.jpg]
