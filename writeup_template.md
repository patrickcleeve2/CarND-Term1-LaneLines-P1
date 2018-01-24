# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps. 

1. Convert the image to grayscale 
2. Apply a Gaussian blur to the image 
3. Apply Canny Edge detection to the image
4. Apply a mask to the region of interest of the image
5. Detect hough lines in the masked image
6. Determine lane lines from hough lines, and draw lane lines on masked image
7. Return the lane line image combined with the real image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by creating a helper function find_lane_lines(). This function took the hough lines as input, and categorised each line into a "left" or "right" lane line based on the gradient of the line. The mean of the set of "left" and "right" line gradients and positions were used to calculate the gradient and position of the "left" and "right" lane lines. These lane lines were then extrapolated to the edge of the region of interest, and drawn over the base image using the draw_lines() function.  

![Lane Line Detection Example 1][./test_images_output/solidWhiteCurve.jpg]
![Lane Line Detection Example 2][./test_images_output/whiteCarLaneSwitch.jpg]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when a line is detected that is not part of the lane markings, such as in the challenge with shadows, or another car passing into the lane. These lines throw off the gradient, and position of the detected lane lines, and cause a very inaccurate 'lane' detection. 

Other shortcoming is the find_lane_lines() function is very verbose, and not likely very efficent. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to constrain measurements of the gradient to a certain range. Given the camera is fixed in the car, the lane lines should only be displayed in a certain range of gradients (i.e. not horizontally). If the pipeline only considered gradients valid, if they fell within a pre-determined range, the classifications of lane lines could be improved, by removing clearly incorrect lane detections. 

The find_lane_lines() function could likely be improved, through a better use of numpy and proper profiling.  

