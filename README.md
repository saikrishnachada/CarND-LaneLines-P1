# **Project1 : Finding Lane Lines on the Road** 

### Objectives 

(1) Develop a pipeline to detect the lane markings on a series of individual images and draw continuous solid lane lines on both sides of the lane.   
(2) Improve the pipeline and try to continuously draw the lane lines on two video datasets.  
(3) Document the procedure along with the necessary further improvements in a written report.   


[//]: # (Image References)

[image1]: ./examples/Before_draw_line().png "Plot"
[image2]: ./test_images_output/solidWhiteCurve.jpg "Plot"
---

### Pipeline description 


The following are the steps that I have used in my pipeline.  
First, I have read the images and converted them to grayscale, in order to provide less information for each pixel.  
Then I have applied gaussian smoothing to reduce image noise.  
Later, I have defined my parameters for canny edge detection. Then I have defined my region of interest and created a mask image. 
In the next step I have performed hough transform on the masked image. Below is the image before performing any changes to draw_line().  

![alt text][image1]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function. 
In the first step, the line segments are separated to either left/right side by verifying if the average of x coordinates
of each line is to the left half of the image or to the right respectively.  Fit lines using np.polyfit() to the x and y 
points on the left and right sides respectively and line form (y=mx+b) is obtained using np.poly1d(). Using the slope and 
intercept from this line, the bottom and top points of the line are calculated. Finally, the lane lines joining these 
points on both left and right side are drawn on the image. Example of the final plot can be seen here.  

![alt text][image2]

Similarly, the above modified draw_lines() function is tested on two video datasets.  
* solidWhiteRight.mp4
* solidYellowLeft.mp4  

Results are found to be satisfactory. 

### Shortcomings in my pipeline


The technique used here to join top and bottom points may not work for roads with curves. Another shortcoming could
be that the pipeline is inefficient to function for change in weather conditions. 


### 3. Possible improvements to my pipeline

The draw_line() function can be further improvised to draw efficient lane lines in the curved roads as well. Advanced hough transform techniques can be used to detect faded lane markings, in adverse weather conditions.
