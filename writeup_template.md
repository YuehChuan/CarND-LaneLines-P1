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

firstly, I want to say that the template has a bug in region_of_interest issue with fillPoly() cv2.fillPoly() function; that may make students feel panic without successful running the template. 
I suggest to approve the pull request soon!(https://github.com/udacity/CarND-LaneLines-P1/issues/35)  thanks frankcarey. 

    +# We need to pass in an array of shapes (each shape is an array of vertices)
    +cv2.fillPoly(mask, [vertices], ignore_mask_color)

Comeup with the result, I didn't take the optinal challenge, because cannot run it with my pipeline.    
My pipeline consisted of process_image() and draw_lines() functions.

process_image() do the pipeline as the class introduced.

Firstly, I converted the images to grayscale, then I do gaussian_blur with kernel size 5 to smooth the piture make 
noisy feature less. 

Secondly,apply canny edge to get edges. 

Thirdly, get trapezoid_region with region of interest function. The reason why not apply region of interest function 
before canny edge. Because the boundary of the mask would be counted into edges.

Then use region_of_interest function to get trapezoid_region. 
Finally apply hough_lines() to get line segements.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
mainly catergorize line segments into different slopes. Then do moving average. 
The result merge line_image and color image in same frame with weighted_img() function.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

In optional challenge, I cannot run my pipeline, but in time constrain, I haven't check it out.
In curve road may fail the algorithm.
I guess is to apply moving average between t-1 frame and t frame.

And my pipeline didn't use the RGB color information,  because identify lane colors will case by case depends on the road situation. We don't want that. 
  
Another shortcoming could be the edge slope is predefine with finetune parameter. It may fail in some cases.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to moving average between t-1 frame and t frame.


