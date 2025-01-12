# **Behavioral Cloning**

## Writeup

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:

* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report

[//]: # (Image References)

[image1]: ./examples/placeholder.png "Model Visualization"

[image2]: ./examples/placeholder.png "Grayscaling"

[image3]: ./examples/placeholder_small.png "Recovery Image"

[image4]: ./examples/placeholder_small.png "Recovery Image"

[image5]: ./examples/placeholder_small.png "Recovery Image"

[image6]: ./examples/placeholder_small.png "Normal Image"

[image7]: ./examples/placeholder_small.png "Flipped Image"

## Rubric Points

### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.

---

### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:

* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* writeup_report.md or writeup_report.pdf summarizing the results

#### 2. Submission includes functional code

Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by
executing

```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline
I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 3x3 filter sizes and depths between 32 and 128 (model.py lines
18-24)

The model includes RELU layers to introduce nonlinearity (code line 20), and the data is normalized in the model using a
Keras lambda layer (code line 18).

In a way the model is very simple: A pretrained model for feature extraction and then a few dense layers for the
regression.

VGG16 was chosen as the pretrained model (TODO: lines) and is easily integrated as it is already part of the Keras
library. It consists of repetitions of two to three 3x3 convolutional layers which are then followed by max pooling
layers. Detailed information about the model can be found [here](https://arxiv.org/pdf/1409.1556.pdf).

The top four layers (3 convolutional, 1 max pooling) were cut off (TODO: lines). Then the output was flattened and after
a dropout layers followed by a dense layer with 256 output notes, and a ReLU activation function. Ot top of this comes
another dropout a second dense layer with 100 output nodes and another ReLU activation. connected to that is the single
output neuron.

#### 2. Attempts to reduce overfitting in the model

Taking a pretrained model and freezing the weights completely prevents overfitting in the feature extraction part of the
network.

In order to reduce overfitting the dense layers on top of the pretrained layers the model contains dropout layers (TODO:
lines) as described above.

The model was trained and validated on different data sets to ensure that the model was not overfitting (TODO lines). If
the validation loss didn't increase significantly for three epochs in a row training is sopped by callback. Also, the up
to this point best performing model gets saved. The model was tested by running it through the simulator and ensuring
that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (TODO: line).

#### 4. Appropriate training data

Unfortunately, I did not manage to play the simulator smoothly via VNC at all. Trying to get it to run locally led also
to a couple of problems. After quite a few frustrating hours, I opted to use only the data that were provided. 

Luckily, the data turned out to be sufficient to get the model working well on the first trek. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the ... I thought this model might be appropriate
because ...

In order to gauge how well the model was working, I split my image and steering angle data into a training and
validation set. I found that my first model had a low mean squared error on the training set but a high mean squared
error on the validation set. This implied that the model was overfitting.

To combat the overfitting, I modified the model so that ...

Then I ...

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots
where the vehicle fell off the track... to improve the driving behavior in these cases, I ....

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers
and layer sizes ...

Here is a visualization of the architecture (note: visualizing the architecture is optional according to the project
rubric)

![alt text][image1]

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example
image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle
would learn to .... These images show what a recovery looks like starting from ... :

![alt text][image3]
![alt text][image4]
![alt text][image5]

Then I repeated this process on track two in order to get more data points.

To augment the data sat, I also flipped images and angles thinking that this would ... For example, here is an image
that has then been flipped:

![alt text][image6]
![alt text][image7]

Etc ....

After the collection process, I had X number of data points. I then preprocessed this data by ...

I finally randomly shuffled the data set and put Y% of the data into a validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under
fitting. The ideal number of epochs was Z as evidenced by ... I used an adam optimizer so that manually training the
learning rate wasn't necessary.
