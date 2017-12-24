## Writeup Template
### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Vehicle Detection Project**

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector.
* Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

[//]: # (Image References)

## [Rubric](https://review.udacity.com/#!/rubrics/513/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Vehicle-Detection/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!

### Histogram of Oriented Gradients (HOG)

#### 1. Explain how (and identify where in your code) you extracted HOG features from the training images.

1. First, I created car and notcar list from the folder vehicles and non vehicles.
2. Then created a hog function with the parameters orient, pixel_per_cell, cells_per_block.
3. Have included the distinctive images of car and notcar images
4. Used and experimented with different color spaces and displayed the hog results of first 10 images.
5. YUV color space provided better results after experimentation with other color spaces
[image1]: ./examples/car_notcar.png




#### 2. Explain how you settled on your final choice of HOG parameters.

I tried various combinations of parameters and experimented with different color spaces.

#### 3. Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them).

1. In the very next step i have trained a linear svm.
2. I have used YUV color space features not including all the color channels and hog features.
[image2]: ./examples/hog_features.png

### Sliding Window Search

#### 1. Describe how (and identify where in your code) you implemented a sliding window search.  How did you decide what scales to search and how much to overlap windows?

I decided to search random window positions at random scales all over the image and came up with this (ok just kidding I didn't actually ;):
1. I have used different lower window position over the image since that's the region of interest.
2. Have used cell_step = 2 to overcome overlap by a factor of 2 by skipping its

[image3]: ./examples/sliding_Window.png

#### 2. Show some examples of test images to demonstrate how your pipeline is working.  What did you do to optimize the performance of your classifier?

Ultimately I searched on two scales using YCrCb 3-channel HOG features plus spatially binned color and histograms of color in the feature vector, which provided a nice result.  experimented with differet scaling values as well as tried different window lengths to get a stable windowed output boxes.

[image4]: ./examples/pipeline.png
---

### Video Implementation

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives.)

https://youtu.be/2a3X3Yhup1g
https://youtu.be/WF0AXQmsyQU

#### 2. Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes.

I recorded the positions of positive detections in each frame of the video.  From the positive detections I created a heatmap and then thresholded that map to identify vehicle positions.  I then used `scipy.ndimage.measurements.label()` to identify individual blobs in the heatmap.  I then assumed each blob corresponded to a vehicle.  I constructed bounding boxes to cover the area of each blob detected.  

Here's an example result showing the heatmap from a series of frames of video, the result of `scipy.ndimage.measurements.label()` and the bounding boxes then overlaid on the last frame of video:
[image5]: ./examples/heatmap.png




[image5]: ./examples/scipy.png
### Here the resulting bounding boxes are drawn onto the last frame in the series:

[image6]: ./examples/bounding_box.png

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
1. the vehicle detection is not smooth enough and there is some disturbances during multiple vehicles
2. However this can be improved by experimenting with the parameters
3. Nearby vehicles detection sometimes takes time, Other than the pipeline successfully detects the vehicles.
