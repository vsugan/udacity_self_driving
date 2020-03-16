# **Finding Lane Lines on the Road** 
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)


[image1]: ./test_images/challenge_img_5.jpg
[image2]: ./test_images_edges/challenge_img_5.jpg
[image3]: ./test_images_output/challenge_img_5.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
The pipeline is very similar to what is described in the lecture. It consists of 
1. grayscaling the image, 
1. Gaussian blur of the image
1. Canny detection of the relevant edges.
1. Remove the edges from portion of the screen which are not likely to be in the current lane.
1. Identifying the straight lines in hough space, where only those lines with more than the threshold points are taken in to consideration. Also, this step includes the function to draw lines where i had added a few customizations for averaging & extrapolation. Averaging is done based on filtering out lines with relevant slopes for the left & right lines to filter out the noise.  This is followed by tracking the lower most & upper most points of the lane for the left & right edges. Once these points are identified, I calculate the slope, so i can extend the line to the bottom most part of the image.
1. The last step is overlapping the identified lane lines on top of the image (same as in the lecture. no change here).

Here is a sample image, with the lanes identified and overlapped on the original image.
![alt text][image3]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
