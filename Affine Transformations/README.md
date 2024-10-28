# Affine Transformations

## Project Overview

In the previous Lab [Contours, Shape & Texture Models](https://github.com/Sani-Abdullahi-Sani/Computer-Vision/tree/main/Contours%2C%20Shape%20%26%20Texture%20Models), we worked with shape models so that we could extract and match the edges of the puzzle pieces. Now that we have the graph representing the puzzle piece connections, we are finally able to solve the puzzle!


## Installation
To run this project, you need to have Python installed along with the following libraries:

- OpenCV
- NumPy
- Matplotlib

You can install the required libraries using pip:

```bash
pip install opencv-python numpy matplotlib
```

## Usage
To apply affine transformations to an image, Below are examples of the transformations that are performed:

- **Translation:** Shifts the image in the x and y directions.
- **Rotation:** Rotates the image around a specified point.
- **Scaling:** Resizes the image by a scaling factor.
- **Shearing:** Skews the image in a specified direction.

## Accessing Data

To access the images, masks, and corner files, please visit the following Google Drive link: [Images, Masks, and Corners](https://drive.google.com/file/d/1geO67J3zbUB-GzITWDRlVb049LpwzZRv/view?usp=sharing).

## Implementation Steps
- **Step 1:** Set Up the `Piece.insert()` Function
  - Update the `self.piece_type` attribute based on the number of connected edges.
  - Iterate through `self.edge_list` to count how many edges are connected to already inserted pieces. Use this count to determine whether the piece is a 'corner', 'edge', or 'interior' piece.

- **Step 2:** Inserting a Corner Piece
  - Use OpenCV functions `cv2.getAffineTransform(·)` and `cv2.warpAffine(·)` to perform the affine transformation.
  - Define `pts_src` and `pts_dst` to map the corner piece coordinates to the canvas coordinates.
  - Update the puzzle piece's image and mask, then blend the piece onto the canvas using the mask.

- **Step 3:** Update Edges after Insertion
  - Implement the `self.update_edges(self, transform)` function to adjust the piece's edge coordinates according to the affine transformation.
  - Ensure that the coordinates are correctly flipped and appended with 1 for homogeneous coordinates.

- **Step 4:** Inserting Interior Pieces
  - Loop through the edges of `self.edge_list` to find connected edges that are already inserted.
  - Construct `pts_src` and `pts_dst` accordingly, then apply the affine transformation as done in Step 2.

- **Step 5:** Inserting Edge Pieces
  - Identify the connected edge and determine the scaling factor for the transformation.
  - Calculate the third point in the canvas coordinates based on the established conditions and insert the piece into the canvas.
  
- **Step 6:** Implementing the Puzzle Solver
  - Open the `run.py` file and create a Puzzle object using `puzzle = Puzzle(MATCH_IMGS)`.
  - Implement a Breadth-First Search (BFS) to solve the puzzle by starting with a corner piece and inserting it into the canvas.
  - Utilize the `Piece.return_edge()` generator function to help loop through edges during the BFS.

## Example
```bash
# Example of inserting a corner piece into the canvas
canvas = np.zeros((800, 700, 3))
corner_piece = puzzle.pieces[3]
corner_piece.insert(canvas)
```

## Conclusion
By completing this lab, you will gain practical experience in using affine transformations for image manipulation and understand how to apply these concepts to solve geometric puzzles in computer vision. Tada! we finally solve the puzzle, and Tino is free.



