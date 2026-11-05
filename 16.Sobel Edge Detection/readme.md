import cv2
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

image_path = 'king.jpg'
try:
    # Load the image and convert to grayscale
    img = cv2.imread(image_path)
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    # Apply Sobel Filter in X direction (detects vertical edges)
    sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3)
    
    # Apply Sobel Filter in Y direction (detects horizontal edges)
    sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3)

    # Convert back to absolute 8-bit values
    abs_sobel_x = cv2.convertScaleAbs(sobel_x)
    abs_sobel_y = cv2.convertScaleAbs(sobel_y)

    # Combine the two gradients to get the overall edge magnitude
    sobel_combined = cv2.addWeighted(abs_sobel_x, 0.5, abs_sobel_y, 0.5, 0)

    # Display the results
    fig, axes = plt.subplots(2, 2, figsize=(14, 10))

    axes[0, 0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
    axes[0, 0].set_title("Original Image")
    axes[0, 0].axis('off')

    axes[0, 1].imshow(abs_sobel_x, cmap='gray')
    axes[0, 1].set_title("Sobel X (Vertical Edges)")
    axes[0, 1].axis('off')

    axes[1, 0].imshow(abs_sobel_y, cmap='gray')
    axes[1, 0].set_title("Sobel Y (Horizontal Edges)")
    axes[1, 0].axis('off')

    axes[1, 1].imshow(sobel_combined, cmap='gray')
    axes[1, 1].set_title("Sobel Combined Gradient Magnitude")
    axes[1, 1].axis('off')

    plt.tight_layout()
    plt.show()
