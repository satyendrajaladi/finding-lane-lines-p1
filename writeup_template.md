# **Finding Lane Lines on the Road** 

## Writeup Template



---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

**Project Pipeline**

1. Color Selection - Grayscale - eliminate almost everything in the image except the lane lines in the grayscale helper function(cv2.cvtColor).

2. Gaussian Blur   - To ensure that only the sharpest edges get through,  a kernel size (5) is applied through the helper function gaussian_blur(cv2.GaussianBlur) is applied Gaussian smoothing / blurring.

3. CannyEdge Detection - Canny edge detection algorithm will turn an image into pure black and white measures the change in connected pixel values. (cv2.Canny) helper function will perform this.

4.Region of Interest (ROI) - The lane detection only happens in a triangular region, which is in front of the car region.

region_of_interest function will call create_vertices helper function which will search and determine the ROI dynamically(lane lines are at the bottom of the image) when the road is straight or turning left or right.the ROI is set at the found points with some buffer to draw the line thickness.

5.Hough Transform will scan the image and detect where pixels form lines,average_lines function takes the output from Hough transform and gives the two solid thick lines which are obtained by grouping positive and negative slopes.


[//]: # (Image References)

[image1]: ./test_images_output/overlayed_lines_1.png "overlayed_lines"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian blur followed by canny edge to convert to black and white,and ROI at the bottom of image which is the front of car portion,and hough tranform to find the lanes and finally drawing  on the single image. 

1. Color Selection - Grayscale - eliminate almost everything in the image except the lane lines in the grayscale helper function(cv2.cvtColor).

2. Gaussian Blur - To ensure that only the sharpest edges get through,  a kernel size (5) is applied through the helper function gaussian_blur(cv2.GaussianBlur) is applied Gaussian smoothing / blurring.

3. CannyEdge Detection - Canny edge detection algorithm will turn an image into pure black and white measures the change in connected pixel values. (cv2.Canny) helper function will perform this.

4.Region of Interest (ROI) - The lane detection only happens in a triangular region, which is in front of the car region.
region_of_interest function will call create_vertices helper function which will search and determine the ROI dynamically(lane lines are at the bottom of the image) when the road is straight or turning left or right.the ROI is set at the found points with some buffer to draw the line thickness.
5.Hough Transform will scan the image and detect where pixels form lines,average_lines function takes the output from Hough transform and gives the two solid thick lines which are obtained by grouping positive and negative slopes.



In order to draw a single line on the left and right lanes, I wrote average_lines function and finally drawing the lines and saving the images in the test_output_images directory using detect_lines function.

 

![overlayed_lines][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is when small lines are detected in the middle of the road, entire Region of Interest becomes erroneous.

Another shortcoming is sometimes lane lines are not detected as part of the region detection process in the create_vertices function.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to create a simpler approach for identifying region of interest accurately.

 
