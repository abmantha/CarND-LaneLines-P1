# **Finding Lane Lines on the Road** 

## Abhishek's Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on my work in this write up. 


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps that is very similar to the series of steps introduced in lecture.

    1. Convert an image to grayscale. 
    2. Apply a Gaussian blur of kernel size 5. 
    3. Apply a Canny edge detection filter with low and high thresholds of 50 and 150 respectively. 
    4. Apply a mask to capture a trapezoidal region of interest in the lower half of the image.
    5. Apply a Hough transform on this masked area to identify lane lines
    6. Draw the final red traffic lanes on image

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
