# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied Gaussian smoothing before using Canny edge detector to get the image of edges, after that, I defined a region of interest in the image of edges since the lane lines often appears in the lower half of the image. To find the proper lines in the ROI, I then applied Hough line detection function.

In order to draw a single line on the left and right lanes, after the above steps were completed,a step was added to connect the lines to get the two parallel lane lines. The lines were first divided into the left lane line and the right lane line based on the slopes they had. I let the lines to draw from the bottom of the image,and let their upper points end at the top of ROI, so I could know the y coordinates of the end points of the full extent of these two lines. The x coordinates were calculated using averaging and extrapolation.

The figure below is the image after the modification: 

![alt text][image1]



### 2. Identify potential shortcomings with your current pipeline


The current pipeline is only for straight lane lines condition, and will fail to find the lane lines under cornering conditions. 

Another shortcoming could be that,the pipeline might fail to detect some images in the vedio,and the accuracy of the lane lines detection result still has room for improvement, because I divide the left and right lane lines simply with the slopes,and the averaging step to get the end points takes all the lines into account. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add some restrictions to choose the lines that participate in the averaging step, in order to improve the detection accuracy of the lane lines 

Another potential improvement could be to make use of the sequence of frames in the vedio to improve the detection rate. Tunning the parameters might also help, but weighted average of the detection results of the several continuous frames may help a lot.
