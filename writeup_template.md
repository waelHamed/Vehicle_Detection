#Udacity's Self-Driving Car Nanodegree Program

##Project 5 - Vehicle Detection and Tracking
The goal of this project is to detect and track vehicles in the scene as this is essential for self-driving cars

## Project steps
This is an explanation of the steps done in the project given a labeled dataset of images including cars and non cars. The dataset is a collection of Images from the Kitti and GTI datasets


### 1- Load data and visualize it.
Plot the dataset of cars and non- cars.

### 2- Convert Image to Histogram of Oriented Gradients (HOG)
I used `skimage.hog()` to calulcate the HOG features for the image after reading it.
I tried extracting the Hog features from 'RGB' color space.

[image1]: ./output_images/Hog.png

### 3- Feature extraction
Next, in the section titled "Extract Features for Input Datasets and Combine, Define Labels Vector, Shuffle and Split¶" I define parameters for HOG feature extraction and extract features for the entire dataset.

### 4- Classification
Train an SVM linear classifier on the extracted features.

### 5- Sliding window
Implement a sliding window that passes through the image, extract features from the window and use the classifier to classify if there is a car inside the window or not. I adapted the method find_cars for each window scale and the rectangles returned from each method call are aggregated. In previous implementations smaller (0.5) scales were explored but found to return too many false positives, and originally the window overlap was set to 50% in both X and Y directions, but an overlap of 75% in the Y direction (yet still 50% in the X direction) produced more redundant true positive detections, which were preferable given the heatmap strategy described below.

[image2]: ./output_images/sliding_windows.png

Because a true positive is typically accompanied by several positive detections, while false positives are typically accompanied by only one or two detections, a combined heatmap and threshold is used to differentiate the two. The add_heat function increments the pixel value (referred to as "heat") of an all-black image the size of the original image at the location of each detection rectangle. Areas encompassed by more overlapping rectangles are assigned higher levels of heat. The following image is the resulting heatmap from the detections in the image above:

[image3]: ./output_images/heatmap.png

### 6- Video
Here is a [link](https://youtu.be/R0ns2lJjJiY) to the video output
``

## Discussion
Regarding the false positives, I think one way for minimizing them is to add more training data for the `not car` class.
I also think that the vision approach alone won't be very robust against different conditions. To make it more robust we can add a kalman filter to track the movement of the cars.
Overall this was an amazing project
