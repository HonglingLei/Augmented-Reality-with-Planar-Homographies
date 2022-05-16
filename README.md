# Augmented Reality with Planar Homographies
In this project, I conducted real-time image and video AR projections through interest point matching and homography estimation. The first step was to find point correspondences with the FAST detector and BRIEF descriptor. Then I estimated homography between the images using the eight-point algorithm. With the computed homography, I'd be able to warp/project an image to the targeted location. 

## Image warping
My code was tested with the following example. A homography was computed between the Computer Vision textbook cover (grey template) and the actual textbook on the table. Below is the matched interest points between the template and target images.

Computer Vision textbook cover:  
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/cv_cover.jpg" height="200" />

Textbook on the table:  
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/cv_desk.png" height="200" /> 

Interest point matching:  
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/matched_points.png" height="200" />

With the estimated homography, we can warp another book cover (e.g. Harry Potter book) to overlay the textbook on the table.

Harry Potter cover:  
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/hp_cover.jpg" height="200" />

Projected result:  
<img src="https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/hp_desk.png" height="200" />

### Some conceptual tips
- **Effects of sigma and ratio:**
  - Sigma is the threshold for corner detection using FAST feature detector. The greater sigma is, the more different the pixel intensities of a corner point and its surrounding points have to be, and thus the fewer corner points are.
  - Ratio is the maximum ratio of distances between first and second closest descriptor in the second set of descriptors. This threshold is useful to filter ambiguous matches between the two descriptor sets. (Source: [scikit.image documentation](https://scikit-image.org/docs/0.15.x/api/skimage.feature.html#skimage.feature.match_descriptors)) The greater the ratio, the more tolerant the matching process, and the more matched pairs/lines.

- **Difference between Harris and FAST:**
  - BRIEF descriptor is a binary descriptor. It randomly extracts pixels surrounding the feature point and compare their grey-scale values p and q (p > q → 1, otherwise 0). Then we get a 256-bit binary string containing information of 256 sets of comparison. Therefore, BRIEF is fast and efficient for storage and matching purposes. It can be combined with FAST to perform rapid feature extraction and description. However, BRIEF is not rotation-invariant. When the picture is rotated, the randomly selected surrounding points are different, and thus the binary vector we get is different. Plus, Hamming distance is only comparing the values at the same index so it will increase accordingly. Therefore, points will match poorly when a picture is too tilted.
  - FAST is more computationally efficient than Harris because it can exclude lots of non- corners by examining only four surrounding pixels (position 1, 5, 9, 13). In contrast, Harris is slow and computationally demanding because of the gradient calculation.

- **Benefits of Hamming distance over Euclidean distance:**
  - For binary vectors, the squares in Euclidean distance are either 0 or 1. Therefore, the sum of those squares is simply the count of differing entries, which is the Hamming distance. Given that these two distances function basically the same in the BRIEF setting, Hamming distance is more computationally efficient than Euclidean.

## Video AR
Now that the single-image AR worked well, I took a step further to implement AR in videos. More specifically, I tracked the Computer Vision text book in each frame of the `book.gif` video, and overlaied each frame of `ar_source.gif` onto the book in `book.gif`. 

Background video `book.gif`:

![book](https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/book.gif)

Content video `ar_source.gif`:

![book](https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/ar_source.gif)

Projected video `ar.gif`:

![book](https://github.com/HonglingLei/Augmented-Reality-with-Planar-Homographies/blob/main/data/ar.gif)
