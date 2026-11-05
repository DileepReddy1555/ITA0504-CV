import cv2
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

image_path = 'king.jpg'
try:
    # Load the image and keep a copy for visualization
    img = cv2.imread(image_path)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    img_corners = img_rgb.copy()
    
    # Convert to grayscale as Harris Corner Detection requires a grayscale float32 image
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    gray = np.float32(gray)
    
    # Apply Harris Corner Detection
    # Parameters: source image, neighborhood size (blockSize), aperture parameter for Sobel (ksize), Harris detector free parameter (k)
    dst = cv2.cornerHarris(gray, blockSize=2, ksize=3, k=0.04)
    
    # Dilate the corner points to make them more visible
    dst = cv2.dilate(dst, None)
    
    # Threshold to identify and mark the strong corners in red on the RGB copy
    img_corners[dst > 0.01 * dst.max()] = [255, 0, 0]
    
    # Display original and corner-detected images
    fig, axes = plt.subplots(1, 2, figsize=(14, 7))
    
    axes[0].imshow(img_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis('off')
    
    axes[1].imshow(img_corners)
    axes[1].set_title("Harris Corner Detection (Corners in Red)")
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()
