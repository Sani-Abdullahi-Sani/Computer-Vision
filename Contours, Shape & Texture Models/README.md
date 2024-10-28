# Lab 4: Contours, Shape & Texture Models

## Overview
In this Lab, we assisted Tino in solving his 48-piece puzzle by reducing the search space for fitting pieces together. Instead of manually attempting to match each piece, we implemented a system to extract the shape information from puzzle piece masks. By utilizing contours and building shape models for each side, we used k-nearest neighbors to naively match puzzle pieces based on their edges.

## Instructions
The goal is to implement a series of steps to extract shape information from puzzle piece masks. This includes:
- Extracting contours from the masks of the puzzle pieces.
- Building shape models for each of the four sides of the puzzle pieces.
- Matching these side models using k-nearest neighbors.

### Steps to Follow:
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

