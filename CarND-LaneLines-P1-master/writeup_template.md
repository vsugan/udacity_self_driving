# **Finding Lane Lines on the Road** 
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)


[image1]: ./test_images/challenge_img_5.jpg
[image2]: ./test_images_edges/challenge_img_5.jpg
[image3]: ./test_images_output/challenge_img_5.jpg.jpg
[image4]: ./test_images_output/solidYellowLeft.jpg.jpg
[challengevideo]: ./test_videos_output/challenge.mp4
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
![alt text][image4]

Here is challenge video result. You can see that the lanes are identified most of the time.
![alt text][challengevideo]

### 2. Identify potential shortcomings with your current pipeline

Current shortcomings observed in the pipeline are:
1. When there are concrete road vs bitumen road and when there is transition between concrete vs bitumen, sometimes, the lines are not clear. The current pipeline mis-identifies those scenarios.
1. The draw_lines method heavily relies on filtering out certain edges from hough space results based on expected slopes. This sometimes leads to lane identified correctly in most cases but misses out in some cases.
1. Places where the lane marking is very light, the guassian blurring needs to change. It cannot be a fixed value since it misses out the lane in some case while picking up noise in other cases.
1. When there are parallel lane like minor markings, current pipeline mis-identifies and along the averaging/exploration, the lane gets extrapolated incorrectly.
1. In turnings, there should more than one line to identify lane. Currently, i'm trying to identify the lane with just one line and that limits the accuracy of the identified lane marking.


### 3. Suggest possible improvements to your pipeline

All the shortcomings listed above can be improved. Specifically 
1. A dynamic guassian blurring depending on the lane marking intensity in the photo, so it helps to filter out the noise appropriately.
1. draw lines method could be improved. The current algorithm is basic and heavily tuned. This sure breaks in new difficult scenarios. draw more than one line for a side of the lane marking could improve accuracy in turnings.  Figure out longer and shorter identified edges and remove the shorter ones if they don't have the x-intercept as the longer line (resolves the parallel lines issue mentioned in #2.4)
