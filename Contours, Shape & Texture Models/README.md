# Lab 4: Contours, Shape & Texture Models

## Overview
In this lab, we aimed to assist Tino in solving his 48-piece puzzle, which he had been attempting to piece together by hand. The sheer number of possible permutations, approximately 9.83531722×10899.83531722×1089 , proved overwhelming. We hypothesized that the unique shapes of the puzzle pieces, as derived from their masks, could be utilized to match corresponding edges effectively. Our objective was to reduce the search space to save Tino from exhaustively trying different permutations. By utilizing contours and building shape models for each side, we used k-nearest neighbors to naively match puzzle pieces based on their edges.

## Instructions
The goal is to implement a series of steps to extract shape information from puzzle piece masks. This includes:
- **Extract Contours**: Identify the contours of all puzzle pieces using the masks.
- **Build Shape Models**: Create models for each side of the puzzle pieces.
- **Naïve Matching**: Use k-nearest neighbors to match puzzle pieces based on their side contours.

## Functions
- `get_puzzle_contour(mask)`: Extracts the largest closed contour from a given binary mask.
- `get_clockwise_contour(contour)`: Returns a contour ordered in a clockwise direction.
- `extract_sides(contour, corners)`: Extracts side contours based on corner information.
- `transform_puzzle_side(contour)`: Translates, scales, and rotates a side contour for normalization.
- `even_spaced_contour(contour, num_points=64)`: Interpolates a contour to have an equal number of evenly spaced points.

## Installation
To set up the environment and install the required packages, run the following command:
```bash
pip3 install natsort numpy imageio scikit-image opencv-python scikit-learn networkx matplotlib
```
## Data Loading
We received a pre-processed dataset, `puzzle_corners_1024x768.zip`, which contained 48 images and corresponding mask pairs. We unzipped the dataset and loaded all images without resizing them.

## Data Loading
```bash
import numpy as np
import imageio
from glob import glob
from skimage import img_as_float32
from natsort import natsorted

path_pairs = list(zip(
    natsorted(glob('./puzzle_corners_1024x768/images-1024x768/*.png')),
    natsorted(glob('./puzzle_corners_1024x768/masks-1024x768/*.png')),
))
imgs = np.array([img_as_float32(imageio.imread(ipath)) for ipath, _ in path_pairs])
msks = np.array([img_as_float32(imageio.imread(mpath)) for _, mpath in path_pairs])
```

## Accessing Data

To access the images, masks, and corner files, please visit the following Google Drive link: [Access Data](https://drive.google.com/file/d/1geO67J3zbUB-GzITWDRlVb049LpwzZRv/view?usp=sharing).

## Finding Contours
The first step involved finding the contours of all puzzle pieces using the masks. A contour was defined as a 2-dimensional data structure consisting of an ordered array of points. We wrote a function called `get_puzzle_contour(mask)` to extract a single contour array of a puzzle piece:

- **Contour Extraction:** We utilized `cv2.findContours` to retrieve contours, sorted them by area to identify the correct one corresponding to the puzzle piece boundary.
- **Ordering Points:** To determine the orientation of the contour points, we implemented `get_clockwise_contour(contour)`, ensuring they were ordered in a clockwise direction.
- **Contour Visualization:** We plotted three reoriented boundaries overlaid on their corresponding RGB puzzle piece images.

## Shape Models
With the normalized boundaries for each puzzle piece, we proceeded to extract the non-closed contours for the sides of the pieces. This involved the following steps:

- **Corner Data Loading:** We loaded JSON corner data for each puzzle piece using the Python `json` package, which provided corner points relative to image dimensions.
- **Side Extraction:** We wrote `extract_sides(contour, corners)` to derive the side contours based on the corner points and the main contour of the puzzle piece.
- **Visualization of Sides:** We plotted the quad formed by the corners and overlaid the extracted sides with distinct colors.

## Normalizing Sides
We normalized the extracted sides to facilitate matching using k-nearest neighbors:

- **Transformation Function:** We implemented `transform_puzzle_side(contour)` to translate, scale, and rotate the side contours.
- **Interpolation:** We wrote `even_spaced_contour(contour, num_points=64)` to perform linear interpolation, ensuring an equal number of evenly spaced points along each side contour.

## Conclusion
By the end of this lab, we successfully implemented a system that reduced the permutation search space for Tino’s puzzle by utilizing contour matching techniques. The project demonstrated the application of computer vision and machine learning methodologies to solve real-world problems.







