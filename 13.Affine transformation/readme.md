import cv2
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

image_path = 'king.jpg'
try:
    # Load the image
    img_array = np.array(Image.open(image_path))
    rows, cols, ch = img_array.shape
    
    # Define three points in the original image
    pts1 = np.float32([[50, 50], [200, 50], [50, 200]])
    # Define where these three points should map to in the output image
    pts2 = np.float32([[10, 100], [200, 50], [100, 250]])
    
    # Calculate the Affine Transformation Matrix
    M = cv2.getAffineTransform(pts1, pts2)
    
    # Apply the Affine Transformation
    affine_img = cv2.warpAffine(img_array, M, (cols, rows))
    
    # Display original vs transformed image
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    axes[0].imshow(img_array)
    axes[0].set_title("Original Image")
    axes[0].axis('off')
    
    axes[1].imshow(affine_img)
    axes[1].set_title("Affine Transformed")
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()
