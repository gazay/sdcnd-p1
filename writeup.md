# **Finding Lane Lines on the Road**

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/normal1.png "Normal"
[image2]: ./test_images_output/normal2.png "Normal extrapolated"
[image3]: ./test_images_output/yellow1.png "Yellow"
[image4]: ./test_images_output/yellow2.png "Yellow with white"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

At first, I've created pipeline similar to the pipeline from lectures. Almost step-by-step:

1. Copy image to not harm original
2. Grayscaling image
3. Apply Gaussian noise
4. Apply canny transform to get edges
5. Apply image mask
6. Get Hough lines
7. Combine original image with image of Hough lines

Here is the result of my first pipeline:

![first pipeline][image1]

Then after I've received nice pictures with partial red lines above white and yellow lane lines,
I've decided to extend draw_lines method to extrapolate those small lines.

I've tried a couple of algorithms for extrapolation – with `np.poly1d` method to get polynome for extrapolated lines
and more simpler – get average slopes of found left and right lines and average centers of them. With last one I could draw a line with just another one point (except center) – in the notebook it is called findX, code is pretty self-described.
The second and simpler algorithm works better than first with `np.poly1d`. Here is the result of its work:

![extrapolated lines][image2]

But then, after I tried this pipeline on the challenge I've decided to change a couple of steps in my pipeline because
it wasn't good enough with yellow lines on not very contrast images/frames. I've added color preprocessing with an accent on yellow and white colors – it works great.

![yellow][image3]
![yellow with white][image4]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when on video with challenge my algorithm can miss some frames as there not enough lines on a region of interest.

Another shortcoming could be that there a lot of hand tunings for every video – image colors,
image size, etc.


### 3. Suggest possible improvements to your pipeline

As I've just finished Udacity's DLND – I've already imagined how it can be improved with
power neural networks. Can't wait to start :)
