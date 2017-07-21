# **Finding Lane Lines on the Road** 

## Abhishek's Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on my work in this write up. 

My code can be found [here](https://github.com/abmantha/CarND-LaneLines-P1/blob/master/P1.ipynb)

[//]: # (Image References)

[image1]: /test_images_output/gray/Gray-solidWhiteCurve.jpg "Grayscale"
[image2]: /test_images_output/gaussian/Gaussian-solidWhiteCurve.jpg "Gaussian"
[image3]: /test_images_output/canny/Canny-solidWhiteCurve.jpg "Canny"
[image4]: /test_images_output/masked/Masked-solidWhiteCurve.jpg "Masked"
[image5]: /test_images_output/hough/Hough-solidWhiteCurve.jpg "Hough"
[image6]: /test_images_output/Lanes-solidWhiteCurve.jpg "Final"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps that is very similar to the series of steps introduced in lecture. Corresponding images are found below. 

    1. Convert an image to grayscale. 
    2. Apply a Gaussian blur of kernel size 5. 
    3. Apply a Canny edge detection filter with low and high thresholds of 50 and 150 respectively. 
    4. Apply a mask to capture a trapezoidal region of interest in the lower half of the image.
    5. Apply a Hough transform on this masked area to identify lane lines
    6. Draw the final red traffic lanes on image

1. Grayscale ![alt text][image1]
2. Gaussian ![alt text][image2]
3. Canny ![alt text][image3]
4. Masked ![alt text][image4]
5. Hough ![alt text][image5]
6. Final ![alt text][image6]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by identifying line segments corresponding to the right and left lanes. Right lanes correspond to line segments of negative slope, while left lanes correspond to line segments of positive slope. I only select slopes that are within a small epsilon value of the maximum and minimum slope values of the segments (corresponding to left and right lane, respectively); in other words, to select line segments that closely resemble the traffic lanes. I also calculate centers, or midpoints, for each of these line selected segments. Using these calculated slopes and midpoints, I calculate the average slopes and midpoints. At this point, I can now use the slope-intercept formula to extrapolate values at the bottom and top of the masked region of interest. Now, I can calculate new (x1, y1) and (x2, y2) points for both right and left lanes. At the end of the function, I draw these new red lines onto the image and return the desired image. 


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming of my current pipeline is that it has difficulty resolving curved lanes of extreme angles. For example, in the Challenge video, my pipeline has difficulty resolving line segments where the curve bends a steeper degree than a typical straight line segment. As a result, my pipeline fails to accurately and consistently draw lanes.

Another shortcoming is that I do not apply any further advanced color masking or segmentation. I attempted to apply some additional selection for yellow (primarily to select yellow lane colors). However, based on the assumption that the camera's position is fixed, I utilized the fact that the lanes appear and are within a (generally speaking) fixed region of interest. This makes for a relatively easy area of detection. However, it will certainly fail to a more generalized case where lanes must be detected outside of that area of interest.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to implement a better strategy to select and calculate slope values in the trapezoidal region of interest corresponding to lanes. I implemented the technique for averaging and extrapolation suggested in this video [Udacity Help](https://www.youtube.com/watch?v=hnXkCiM2RSg&list=PLAwxTw4SYaPkz3HerxrHlu1Seq8ZA7-5P&index=1&t=4s). However, I think I would have more success if I used some sort of second/third-order regression model to easily fit a values to a closely matching lane line. 

Another potential improvement could be to account for color variations in the road. For example, the Challenge video's change in road color, amongst other reasons, caused my pipeline to fail. This is certainly an opportunity for improvement. 

Finally, I am incredibly grateful for this first project. Though there are many areas for improvement, I'm very excited for all that I will learn in the coming months. Thank you!
