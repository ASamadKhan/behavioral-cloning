# **Behavioral Cloning** 

[//]: # (Image References)

[image1]: ./images/nvidiamodel.png "NVIDIA"
[image2]: ./images/final_model.png "Final Model"
[image3]: ./images/center.png "Center Image"
[image4]: ./images/brightness.png "Recovery Image"
[image5]: ./images/shift.png "Recovery Image"
[image6]: ./images/shadow.png "shadow Image"
[image7]: ./images/flipping.png "Flipped Image"
[image8]: ./images/crop.png "Cropping"
[image9]: ./images/resize.png "Resize"


---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* New Model.ipynb containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* README.md for summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The New Model.ipynb file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 5x5, 3x3  filter sizes and depths between 24 and 64 (last code cell in New Model.ipynb) 

The model includes ELU to introduce nonlinearity (last code cell), and the data is normalized in the model using a Keras lambda layer (last code cell). 

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layer in order to reduce overfitting (New Model.ipynb last code cell). 

Not only model was trained and validated on different data sets but augmentation was used to ensure that the model was not overfitting (code line 10-16). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the 1st track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (last code cell).

#### 4. Appropriate training data

Sample data provided by the udacity was used augmentation.
For details about how I created the training data, see the next section. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach



My first step was to use a convolution neural network model similar to the End to End Learning for Self-Driving Cars from NVidia.   
![alt text][image1]

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that model was overfitting and taking a lot of time for training. to reduce the over all time in trainig I cropeed and resized my input images into 64x64.

To combat the overfitting, I modified the model by introducing dropout.

The final step was to run the simulator to see how well the car was driving around track one. There were a one spot where the vehicle touched the line of the track. to improve the driving behavior in that cases, I dropped the last convolution layer.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...

Here is a visualization of the architecture 

![alt text][image2]

#### 3. Creation of the Training Set & Training Process

In the first place I recrded more than two laps using the first track. I was not using the analog joystick so i was ot very happy with the data and in fact It was not helping me with the learning too. Then I decided to use udacity sample data.
Here is one of the image from the centre camera.

![alt text][image3]
<br>
To produce more data I augmented the data.<br>
To tackle day and night conditio random brightness was introduced. This is done first by converting image into HLS channel. then L channel was scalled with random value of brightness. below image shows how random brightness is introduced. 

![alt text][image4]
<br>
To simulate the effect of car being at different position on the road camera images are shifted horizentally. This is done by adding an offset correspondin to the shift to the steering angle. images are also shifted vertically by random number by giving an effect of driving up or down the slope.
![alt text][image5]
<br>
Shadow is introduced at random position in the image. below figure shows the effect of shadowing. 
![alt text][image6]
<br>
To augment the data more , I also flipped images and angles. here is an image that has been flipped:
![alt text][image7]
<br>
to remove horizon and car's hood 50 pixels from the top and 25 pixels from the bottom were cropped. This is due to the fact that we do not need it for decision making. 
![alt text][image8]
<br>
In the last stage image was resized to 64*64.
<br>
![alt text][image9]

since there are three camera views so at any single time I am randomly picking only one view.

I finally randomly shuffled the data set and put 20% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The number of eoches were varied and the best result were obtained with number_epoches=3.  
<br>Here is the youtube video link how the model is performing on the first track.
https://www.youtube.com/watch?v=wd6018t4Tto&feature=youtu.be
<br>
The model can be further improved by trying different various parameters. Due to time constraints I could not test more models. I faced a lot of diffuculties as I have to train it on my PC. but, I enjoyed it alot.
