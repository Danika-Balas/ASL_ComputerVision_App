# ASL Computer Vision App
An iOS app built using the CoreML framework and a CNN model developed with CreateML. The app classifies images of letters in the American Sign Language (ASL) alphabet.

## Overview
American Sign Language (ASL) is used by an estimated [250,000-500,000 people](https://www.gallaudet.edu/documents/Research-Support-and-International-Affairs/ASL_Users.pdf) in the US. I used Apple's [CreateML](https://developer.apple.com/documentation/createml) and data from Kaggle(https://www.kaggle.com/grassknoted/asl-alphabet) to train a Convolutional Neural Network
The app is intended as a proof-of-concept for using computer vision to interpret sign language.

<p float="left">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/A_test.png" width="288" />
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/B_test_left.png" width="288" /> 
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/C_test.png" width="288" />
</p>

## Table of Contents
* [Overview](#Overview)
* [Table of Contents](#Table-of-Contents)
* [Using this Repository](#Using-this-Repository)
* [Data](#Data)

## Using this Repository
1. Clone this repository
2. Open Vision+ML Example.xcodeproj in Xcode
3. Select a simulator or use your own iOS edge device
4. Compile the project and deploy it to your iOS device of choice
5. If you are using the simulator, add images of signed letters by dragging and dropping them onto the simulator
6. Make inferences using the Vision+ML app

## Data 
In order to train the image classification model, I combined two datasets from Kaggle.

I randomly sampled half the images from [this dataset](https://www.kaggle.com/grassknoted/asl-alphabet) in order to reduce the time and computational resources needed to train the model. I then supplemented them with images from [this small dataset](https://www.kaggle.com/danrasband/asl-alphabet-test) in order increase the variety within training set.

The training set consisted of 1,515 images for each class. There are 28 classes, one for each of the 26 letters in the ASL alphabet (A-Z) plus *SPACE* and *NOTHING*. Each image is 200x200 pixels.
