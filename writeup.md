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
[image2]: ./test_images_output/greyImg.pgn  "Gray"
[image3]: ./test_images_output/blurr.png  "Blurr"
[image4]: ./test_images_output/edgesImg.png  "Edges"
[image5]: ./test_images_output/maskedEdgesImg.png  "MaskedEdges"
[image6]: ./test_images_output/lanes.png  "Lanes"
[image7]: ./test_images_output/solidWhiteRight.jpg  "Result"





---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps: 
1. Convert the original RGB image to gray scale
![alt text][image2]

2. Apply a Gaussian smoothing / blurring to the gray image. 
![alt text][image3]

3. Apply a Canny Edge Detection algorithm to the smoothed image.  
![alt text][image4]

4. Limit the area of interest from the resulting image on previous step by defining a poligon and masking the result.
![alt text][image5]

5. Apply Hough to resulting image from previous step. Parameters must be adjusted to reduce noise and return lines of interest only (lane lines edges)
6. Use an algorithm to draw thicker and continuous lines on top of the lanes. The drawing algorithm - draw_lines() method was modified to execute the following:
	- For each detected line, calculate the slope of the line. 
		- If the slope in negative, this line is related to the left lane. 
		- If the slope is positive, the line is related to the right lane.  
	- Calculate the mean slope of all lines from each lane,
	- Extrapolate lines from each lane so they intersect.
	- Use a proper tickness to draw the lane
![alt text][image6]

7. Overlay the original image and the resulting image from previous step. 
![alt text][image7]




### 2. Identify potential shortcomings with your current pipeline

The current solution is very basic and have not been tested in many different image samples. The following are a couple of potencial shorcomings of the current solution:
- Sharp turns to the left or right. Lines may not be detected properly by the Hough Detection.  Average slope may cause mistakes on the draw line.  
- Shades and different brightness may casue the algorithm to fail. 



### 3. Suggest possible improvements to your pipeline

Some of the Hough parameters could be fine-tuned to be more robust to different scenarios. 
The are of interest of the image could be further limited to improve reduce the possibility of detecting lines not related to lanes. 

