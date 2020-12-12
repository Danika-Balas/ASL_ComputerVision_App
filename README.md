# ASL Computer Vision App
An iOS app built using the CoreML framework and a CNN model developed with CreateML. The app classifies images of letters in the American Sign Language (ASL) alphabet.

## Overview
American Sign Language (ASL) is used by an estimated [250,000-500,000 people](https://www.gallaudet.edu/documents/Research-Support-and-International-Affairs/ASL_Users.pdf) in the US. I used Apple's [CreateML](https://developer.apple.com/documentation/createml) and data from Kaggle(https://www.kaggle.com/grassknoted/asl-alphabet) to train a Convolutional Neural Network.

The app is intended as a proof-of-concept for using computer vision to interpret sign language.

<p float="left">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/A_test.png" width="256" />
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/B_test_left.png" width="256" /> 
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/C_test.png" width="256" />
</p>

## Table of Contents
* [Overview](#Overview)
* [Table of Contents](#Table-of-Contents)
* [Accessing the App](#Accessing-the-App)
* [Data](#Data)
* [Training the Model](#Training-the-Model)
* [Model Performance](#Model-Performance)
* [Adding Model to an iOS App](#Adding-Model-to-an-iOS-App)
* [Future Directions](#Future-Directions)

## Accessing the App
1. Clone this repository
2. Open Vision+ML Example.xcodeproj in Xcode
3. Select a simulator or use your own iOS edge device
4. Compile the project and deploy it to your iOS device of choice
5. If you are using the simulator, add images of signed letters by dragging and dropping them onto the simulator
6. Make inferences using the Vision+ML app

## Data 
In order to train the image classification model, I combined two datasets from Kaggle.

I randomly sampled half the images from [this dataset](https://www.kaggle.com/grassknoted/asl-alphabet) in order to reduce the time and computational resources needed to train the model. I then supplemented them with images from [this small dataset](https://www.kaggle.com/danrasband/asl-alphabet-test) in order to increase the variety of backgrounds within the training set images.

The training set consists of 1,515 images for each class. Each image is 200x200 pixels. There are 28 classes, one for each of the 26 letters in the ASL alphabet plus *SPACE* and *NOTHING*. In ASL, most of the letters use static signs, but the letters J and Z involve motions. For the purposes of this model, J and Z are represented by images of hands in the starting position of these motions.

<p float="left">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/ASL-Alphabet-ASDC.jpg" width="768" />
</p>


## Training the Model
I used Apple's AutoML tool, [Create ML](https://developer.apple.com/documentation/createml/creating_an_image_classifier_model), to develop the ASL alphabet image classifier.

Create ML automatically divided the training data into a training set and a validation set.

I used data augmentation to expand the training dataset. I added flipped images because all of the training images portray right hands and I wanted the model to work on letters signed by right or left hands. I added images with different exposure because many of training images have poor lighting and I wanted the model to work in environments with a variety of lighting.

I trained the model for 200 iterations.

<p float="center">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/model_training.png" width="384" />
</p>

## Model Performance
The model had an accuracy of 97.1% on the training data, 94.8% on the validation data, and 96.0% on the testing data.

The testing data was pulled from the same pool as the training data (without any overlap in individual samples), so it is not surprising that it performed about as well on the testing data as the training and validation data.

Accuracy was much less consistent for novel images. The model likely overfit to the training data. In general, the model performed better on images of right hand signs and signs in dimmer lighting.

<p float="center">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/model_evaluation.png" width="768" />
</p>

## Adding Model to an iOS App
After training the model in Create ML, I downloaded it as a .mlmodel file. I also downloaded a [sample app](https://developer.apple.com/documentation/vision/classifying_images_with_vision_and_core_ml) from Apple which combines the [Vision](https://developer.apple.com/documentation/vision) and [Core ML](https://developer.apple.com/documentation/coreml) frameworks.

I used Xcode to add the custom ASL alphabet model to the app and make some minor changes to the display of the app. 

Finally, I compiled the project. With the newly created app, I can make inferences with novel images at using any iOS device as an edge device.

<p float="left">
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/X_test.png" width="256" />
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/Y_test.png" width="256" /> 
  <img src="https://github.com/Danika-Balas/ASL_ComputerVision_App/blob/main/images/Z_test.png" width="256" />
</p>

## Future Directions
I would start by making the model itself more robust. The model would benefit from expanding the training dataset to include images with a larger variety of:
* Lighting
* Skin tones
* Genders
* Backgrounds (indoors and outdoors)
* Scales
* Resolutions
* Angles
The training data should also be more balanced between right-handed and left-handed signs. 

CreateML worked very well for this project, and the pipeline was very smooth. However, a model that used transfer learning from a pre-trained model that is more specific to hands or hand signals would perform better. CreateML uses transfer learning, but Apple does not share information about the pre-trained models it uses, and it is not very customizable. 

I developed model with TensorFlow using transfer learning, and it performed better on novel images. I was able to use [coremltools](https://coremltools.readme.io/docs) to convert the model from .h5 to .mlmodel format. However, I ran into errors when I attempted to use this model in the Vision+ML app. Coremltools is also only supported by older versions of TensorFlow (v1) and Keras (v2.2.4).

The ASL alphabet app is a prototype because, realistically, people could type to communicate in most of the instances where the app could be used. This app would be a lot more powerful with a wider variety of classes such as words or phrases rather than letters. It would also be a lot more useful if it could use live video as input. The app could then function as a live interpreter, which would be very useful.
