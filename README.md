#Finding Lane Lines - Project Write-Up

This is my first project in the Self-Driving Car Nanodegree Program where, given images and videos taken from the front camera of a car, I detect the lane lines on the road and highlight them in the videos and images. To see my code please look at the Finding_Lane_Lines_Project.ipynb Jupyter Notebook in the root directory of this repository. I was also able to draw the lane lines on videos of a car driving on a road. These videos can be found in the output_videos folder.

***

###Step One - Grayscale & Gaussian Blur The Image

By removing the colors from the image it is easier to detect the edges of the lane lines using the Canny Edge Detection algorithm.

After we grayscale we apply the Gaussian Blur. It is important to blur the image slightly so that we can classify the lane lines without worrying about extra noise. However, it is important that we don't blur it too much because then we might miss important details, like when the lane line is a dashed line instead of a solid one.

-

###Step Two - Canny Edge Detection

Using the Canny Edge Detection algorithm that is defined in the cv2 library we can detect the edges of objects in the image by looking at the gradient. The threshold I used was between 50 and 150 so that the algorithm will first look at pixels above the 150 threshold and discard pixels below the 50 threshold. After this it will include the pixels between 50 and 150 as long as they are connected to strong edges.

-

###Step Three - Mask The Image

The car should not be concerned with objects that are not on the road in this case, so I masked the image to only look at the road in front of it. I did this by defining the vertices of a shape that I mask the image with.

-

###Step Four - Draw The Lines

The most difficult part of this project for me was drawing the lane lines on top of the image. To do this I used the Hough Lines algorithm to filter my grayscaled, blurred image so it only displayed the lines that has a mimimum length of 18, a threshold of 22, and a maximum line gap of 1. This left me with only the lines that were large enough to be the lane lines.

After this I called the Draw Lines function in the Hough Lines function that:

- took the Hough Lines as input
- calculated the slopes of every line
- filtered our lines that had slopes that were to large or small
- put the left lane slopes and the right lane slopes into their own separate lists
- got the mean of all of the slopes and intercepts recorded in my lists
- used the average slopes to generate the lines

-

###Step 5 - Draw the lines and return the image

After I had the lane lines selected in the image I drew those lines on top of the original image and returned the value.

***

###What I Learned

I had never been exposed to image processing in python before this project, so learning how to manipulate pixels and how to preform thresholding was really exciting. Also seeing how all of the algorithms that I learned about work together was really cool. I am excited to learn more.
