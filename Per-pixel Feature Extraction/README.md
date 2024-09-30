# Lab 2: Per-pixel Feature Extraction

## Overview

In this lab, we enhanced our background classifiers for Tino by implementing more sophisticated feature extraction techniques. Building upon our previous work (Handcrafted Features), we introduced additional filters including the Gaussian, Laplacian of Gaussian (LoG), and Difference of Gaussian (DoG) filters. We also explored the rotationally invariant MR8 features and other feature extraction methods such as Local Binary Patterns (LBPs), Haar filters, and textons.

## Objectives

- To implement Gaussian, LoG, and DoG filters for feature extraction.
- To derive the MR8 features from the RFS filter bank.
- To apply Local Binary Patterns and Haar filters on the image.
- To perform clustering and classification using K-Means and logistic regression.

## Requirements

- Python (with libraries such as NumPy, OpenCV, scikit-image, and Matplotlib)
- An RGB image for testing and feature extraction
- Familiarity with convolution operations

## Methodology

### 1. Additional Filters

Implement the following filters manually for the RGB image:

- **Gaussian Filter:** 
- **Laplacian of Gaussian (LoG) Filter:** 
- **Difference of Gaussian (DoG) Filter:** 

### 2. RFS/MR8 Filter Banks

Create a function that generates the RFS filter bank, which includes Gaussian and LoG filters, as well as rotated Gaussian edge and bar filters based on the hyper-parameters \((\sigma_x, \sigma_y)\) and \(\theta\). The filters will be applied to extract MR8 features.

### 3. Local Binary Patterns and Haar Filters

- Implement the Local Binary Pattern filter with various radii (4, 8, 16, 24, 32).
- Calculate integral images for each channel of the original RGB image.
- Apply a checkered Haar filter to the image.

### 4. Textons and Classification

- Apply the feature extraction methods and cluster pixels using K-Means (4 clusters).
- Replace pixels with their corresponding centroids and display the clustered image.
- Train a statistical pixel classifier and evaluate the model's accuracy on test data.
- Incorporate MR8 features into the classifier and assess improvements in accuracy.

## Results
- From our experiments, including logistic regression with all features, PCA transformation, and feature selection with grid search, it is evident that the model using all features consistently delivers the best performance metrics. PCA did not show significant improvements and led to decreased performance on the test set. Therefore, based on these results, the model utilizing all features remains the most effective.


## Conclusion

This lab enhances our understanding of feature extraction techniques and their application in building robust background classifiers. The methods developed in this lab will serve as foundational techniques for future labs and projects.



