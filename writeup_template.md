#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[solidWhiteCurvewoa]: ./linesWithoutAverage/HoughLines_solidWhiteCurve.jpg "solidWhiteCurve without average"
[solidWhiteRightwoa]: ./linesWithoutAverage/HoughLines_solidWhiteRight.jpg "solidWhiteRight without average"
[solidYellowCurvewoa]: ./linesWithoutAverage/HoughLines_solidYellowCurve.jpg "solidYellowCurve without average"
[solidYellowCurve2woa]: ./linesWithoutAverage/HoughLines_solidYellowCurve2.jpg "solidYellowCurve2 without average"
[solidYellowLeftwoa]: ./linesWithoutAverage/HoughLines_solidYellowLeft.jpg "solidYellowLeft without average"
[whiteCarLaneSwitchwoa]: ./linesWithoutAverage/HoughLines_whiteCarLaneSwitch.jpg "whiteCarLaneSwitch without average"
[solidWhiteCurve]: ./linesWithAverage/AveragedHoughLines_solidWhiteCurve.jpg "solidWhiteCurve with average"
[solidWhiteRight]: ./linesWithAverage/AveragedHoughLines_solidWhiteRight.jpg "solidWhiteRight with average"
[solidYellowCurve]: ./linesWithAverage/AveragedHoughLines_solidYellowCurve.jpg "solidYellowCurve with average"
[solidYellowCurve2]: ./linesWithAverage/AveragedHoughLines_solidYellowCurve2.jpg "solidYellowCurve2 with average"
[solidYellowLeft]: ./linesWithAverage/AveragedHoughLines_solidYellowLeft.jpg "solidYellowLeft with average"
[whiteCarLaneSwitch]: ./linesWithAverage/AveragedHoughLines_whiteCarLaneSwitch.jpg "whiteCarLaneSwitch with average"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.


My pipeline consisted of 6 steps. First, I calculate the vertices for the `region_of_interest` function as this is a static process for a given image.
Second, I converted the images to grayscale, then I apply the canny transformation to get the edges. Afterwards, I apply an image mask with the `region_of_interest` function, the in step 1 calculated vertices and the image. The final output is computed by the provided `hough_lines` function.

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by separating the lines by their slope and store the slope and lines in lists for the right and left lane. Afterwards, I calculate the average slope and the x,y position for both lines. Then I define left and right line pairs. To draw a "stable" line from the bottom of the image, I define the a nearly stable x for the left and right lane at the bottom. With all this information, I draw each line separately.

| Images without average and bottom x position | Images with average and bottom x position |
|:---:|:---:|
| ![alt text][solidWhiteCurvewoa] | ![alt text][solidWhiteCurve] |
| ![alt text][solidWhiteRightwoa] | ![alt text][solidWhiteRight] |
| ![alt text][solidYellowCurvewoa] | ![alt text][solidYellowCurve] |
| ![alt text][solidYellowCurve2woa] | ![alt text][solidYellowCurve2] |
| ![alt text][solidYellowLeftwoa] | ![alt text][solidYellowLeft] |
| ![alt text][whiteCarLaneSwitchwoa] | ![alt text][whiteCarLaneSwitch] |


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the pipeline is used in a curve, like you can see in the challenge.mp4 video. The calculated averages does not take in count if the vehicle is driving in a a curve and therefore does not draw a curved line.

Another shortcoming could be that it does not reject outliniers. Without the outlines rejection, the calculated average line will not always be the one on the video.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to reject outlines. With this improvement, the detected line will be more accurate to the real one.

Another potential improvement could be to calculate using the cv2 `polylines` function or use line with each pair of consecutives points.