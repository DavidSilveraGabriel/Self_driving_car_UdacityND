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

My pipeline is a mix of all the code we saw in the course and the functions that were provided by the P1 template such as ```hough_lines ()``` or ```weighted_img ()``` so at first I started copying and pasting parts of code from the course exercises (the code is in exercises.ipynb), after getting an idea of how to work with all the code and what the outputs were, I started to build the ```pipe()``` function until I got the expected output, but I ran into a problem that was at the end of the function where I put it to return ```plt.imshow (weighted_img (lines_edges, image))``` which generated problems when using it in video, corrected it in the following function called process_image () where it simply returns the result saved in ``` lines_edges ```

![output](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/blob/master/P1-master/output_img.png)


### 2. Identify potential shortcomings with your current pipeline


some deficiencies can be seen in the following video:
[![Watch the video](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/blob/master/P1-master/output_img.png)](https://github.com/DavidSilveraGabriel/Self_driving_car_UdacityND/blob/master/P1-master/test_videos_output/challenge.mp4)
as you can see the algorithm cannot adapt to the curves


### 3. Suggest possible improvements to your pipeline

The possible improvements that occur to me are playing with the hyperparameters to try to improve the precision and the delineation of the lines drawn. :sweat_smile:
