# ASL ComputerVision App
An iOS app built using the CoreML framework and a CNN model developed with CreateML. The app classifies images of letters in the American Sign Language (ASL) alphabet.

## Overview
American Sign Language (ASL) is used by x people. I used Apple's [CreateML](https://developer.apple.com/documentation/createml) and data from Kaggle(https://www.kaggle.com/grassknoted/asl-alphabet) to train a Convolutional Neural Network
The app is intended as a proof-of-concept for using computer vision to interpret sign language.

<p float="left">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/A_test.png" width="288" />
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/B_test.png" width="288" /> 
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/C_test.png" width="288" />
</p>

## Table of Contents
* [Overview](#Overview)
* [Table of Contents](#Table-of-Contents)
* [Data](#Data)
* [Performance Evaluation](#Performance-Evaluation)

## Data 
In order to train the image classification model, I combined two datasets from Kaggle.

I randomly sampled half the images from [this dataset](https://www.kaggle.com/grassknoted/asl-alphabet) in order to reduce the time and computational resources needed to train the model. I then supplemented them with images from this small dataset in order increase the variety within training set.

The training set consisted of 1,515 images for each class. There are 28 classes, one for each of the 26 letters in the ASL alphabet plus *SPACE* and *NOTHING*. Each image is 200x200 pixels.

## Performance Evaluation
Coming soon
