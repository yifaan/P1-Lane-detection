#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/edge.jpg "edge"
[image2]: ./test_images/combined_color.jpg "combined_color"
[image3]: ./test_images/mask.jpg "mask"
[image4]: ./test_images/result.jpg "result"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

**Step 1:** Edge detection 
use OpenCV edge detection	
![alt text][image1]

**Step 2:** Color detection 
detect white and yellow color in image in HSV colorspace 

**Step 3:** Dilate color image and combine with edge image

**Step 4:** combine Edge and Color image 
Logic OR for yellow and white, and logic AND between color and edge 
![alt text][image2]


**Step 5:** add Polygon mask 
![alt text][image3]

**Step 6:** Hough transfrom to find all lines

**Step 7:** Use Kmeans to group line segment into two cluster w.r.t angle

**Step 8:** For each cluster, calculate $\theta$ and d for each segment, and take weighted average w.r.t length of the segments

**Step 9:** Using the calculated $\theta$, d to find start and endpoint of line

**Step 10:** Draw Line

![alt text][image4]


###2. Identify potential shortcomings with your current pipeline


Color detection is not robust now.

Using weighted average to fit line is not robust to outlier. 

The result video is not smooth.

###3. Suggest possible improvements to your pipeline

Create gaussian model for white and yellow color detector, so the assignment would be more soft. 

Maybe after clustering, using RANSAC to fit line. It is more robust than simple linear regression.

Add low pass filter to make the line detection result smoother
