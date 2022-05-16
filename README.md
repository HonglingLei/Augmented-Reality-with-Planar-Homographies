# Augmented Reality with Planar Homographies
In this project, I conducted real-time image and video AR projections through interest point matching and homography estimation. The first step was to find point correspondences with the FAST detector and BRIEF descriptor. Then I estimated homography between the images using the eight-point algorithm. With the computed homography, I'd be able to warp/project an image to the targeted location. 

My code was tested with the following example. A homography was computed between the Computer Vision textbook cover (grey template) and the actual textbook on the table. Below is the matched interest points between the template and target images.

Computer Vision textbook cover:
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/cv_cover.jpg" height="200" />

Textbook on the table:
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/cv_desk.png" height="200" /> 

Interest point matching:
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/matched_points.png" height="200" />

- Effects of sigma and ratio:
    - Sigma is the threshold for corner detection using FAST feature detector. The greater sigma is, the more different the pixel intensities of a corner point and its surrounding points have to be, and thus the fewer corner points are.
    - Ratio is the maximum ratio of distances between first and second closest descriptor in the second set of descriptors. This threshold is useful to filter ambiguous matches between the two descriptor sets. (Source: scikit.image documentation: [https://scikit-image.org/docs/0.15.x/api/skimage.feature.html#skimage.feature.match_descriptors](https://scikit-image.org/docs/0.15.x/api/skimage.feature.html#skimage.feature.match_descriptors)) The greater the ratio, the more tolerant the matching process, and the more matched pairs/lines.
