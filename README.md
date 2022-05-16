# Augmented Reality with Planar Homographies
In this project, I conducted real-time image and video AR projections through interest point matching and homography estimation. The first step was to find point correspondences with the FAST detector and BRIEF descriptor. Then I estimated homography between the images using the eight-point algorithm. With the computed homography, I'd be able to warp/project an image to the targeted location. 

My code was tested with the following example. A homography was computed between the Computer Vision textbook cover (grey template) and the actual textbook on the table. Below is the matched interest points between the template and target images.
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/cv_cover.jpg" width="30%" style="display: block; margin: auto;" />
