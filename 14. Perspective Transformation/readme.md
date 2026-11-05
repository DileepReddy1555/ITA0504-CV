import cv2
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

image_path = 'king.jpg'
try:
    # Load the image
    img_array = np.array(Image.open(image_path))
    rows, cols, ch = img_array.shape
    
    # For perspective transformation, we need 4 control points
    # Defining 4 source points (corners of the original image)
    pts1 = np.float32([[0, 0], [cols - 1, 0], [0, rows - 1], [cols - 1, rows - 1]])
    
    # Defining where these 4 points should map to in the destination image to create perspective perspective
    pts2 = np.float32([
        [cols * 0.1, rows * 0.2],        # Top-left moves inward and down
        [cols * 0.9, rows * 0.05],       # Top-right moves slightly inward and up
        [cols * 0.05, rows * 0.95],      # Bottom-left moves slightly inward
        [cols * 0.95, rows * 0.8]        # Bottom-right moves inward and up
    ])
    
    # Calculate the perspective transformation matrix
    M_perspective = cv2.getPerspectiveTransform(pts1, pts2)
    
    # Apply warpPerspective
    perspective_img = cv2.warpPerspective(img_array, M_perspective, (cols, rows))
    
    # Display original vs perspective-transformed image
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    axes[0].imshow(img_array)
    axes[0].set_title("Original Image")
    axes[0].axis('off')
    
    axes[1].imshow(perspective_img)
    axes[1].set_title("Perspective Transformed")
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()
except FileNotFoundError:
    print(f"Could not find '{image_path}'. Please run the first cell to upload it first.")
