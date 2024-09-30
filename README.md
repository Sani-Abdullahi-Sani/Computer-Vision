# Puzzle Piece Segmentation and Classification Using Handcrafted Features: Image Processing Lab

## Overview
In this Lab, we implemented a robust handcrafted feature engineering pipeline designed to extract informative features from images for the classification task. The features were carefully selected to capture both color and edge information, which are crucial for distinguishing between foreground (puzzle pieces) and background pixels.

## 1. Introduction: Meet Tino
We helped Quarantino ("Tino") solve puzzles more efficiently by building a system that will eventually help him assemble puzzles. The first step involves segmentation of the puzzle pieces from the background.

## 2. Data and Libraries
You’re provided with three images and their corresponding masks. The masks contain labels indicating which pixels belong to the puzzle pieces and which belong to the background.

## Libraries you will need for this lab:
- OpenCV (cv2)
- NumPy (np)
- SciPy (scipy.stats)
- Scikit-Image (skimage)
- ImageIO (imageio)
- mpmath
- Matplotlib (plt)
- Seaborn (sns)
- Python Image Library (PIL)

## 3. Reading and Displaying Images
We begin by loading the provided images and masks. After reading the images using OpenCV (cv2), We then:

- Swap the image channels from BGR (OpenCV default) to RGB.
- Convert the images to grayscale using skimage.color.rgb2gray.
- Convert the images to HSV color space using skimage.color.rgb2hsv.
- we visualize these images using plt.imshow() to observe any color anomalies or differences when switching between color spaces.

## 4. Descriptive Statistics
For image-35 which is the Train image, we perform several analyses to gather insights into the image and mask properties:

- Width and height: Extract the dimensions of the image.
- White pixels: Count the number of white pixels in the mask, indicating puzzle piece pixels.
- Grayscale analysis: Calculate statistics on the grayscale version of the image:
- Maximum pixel value (for the entire image and just the puzzle pixels).
- Mean and variance for puzzle piece and background pixels.
- We also visualize histograms for the red, green, blue, and grayscale channels using the seaborn library, both for the image and the mask. Additionally, we use Kernel Density Estimates (KDE) to smooth these histograms.

## 5. Background Classifier
This is where the core task begins—building a classifier to distinguish between background and puzzle pixels.

### Key Tasks:
- Convolution Function: Implement a custom convolution function that applies a filter/kernel to an image. Compare the results with OpenCV's cv2.filter2D function.
- Feature Extraction: Extract 15 features for each pixel, including RGB, HSV values, and results from applying Prewitt and Laplacian filters.

**Bayes' Rule Classifier:** Calculate the mean and covariance matrix for these features and use Bayes' rule to classify pixels as foreground (puzzle) or background.

**Classifier Evaluation:**
We train the classifier on the training image and calculate various metrics:

- Accuracy
- Precision
- Recall
- F1 Score
- In addition, we plot the ROC curve and investigate how adjusting the probability threshold affects performance.

**Intersection-over-Union (IoU):** Calculate the IoU score to measure the model's segmentation performance.
**Feature Selection:** We tried different sets of features and determine which set gives the best performance on the validation image. we then selected the best feature set, and apply the model to the test image and compute the final performance metrics.


## 6. Deliverable
Jupyter Notebook containing:

- Clear, organized sections for each task.
- The code and results for each step.
- A reflection on the model’s performance, common errors, and suggestions for improvement.
