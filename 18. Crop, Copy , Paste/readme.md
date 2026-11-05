import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = 'king.jpg'
try:
    # Load the image
    img = cv2.imread(image_path)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    h, w, c = img_rgb.shape

    # Define coordinates for Region of Interest (ROI)
    # We'll take a central bounding box based on the image's dimensions
    roi_y1, roi_y2 = int(h * 0.3), int(h * 0.6)
    roi_x1, roi_x2 = int(w * 0.3), int(w * 0.6)

    # 1. Crop (Select ROI)
    roi = img_rgb[roi_y1:roi_y2, roi_x1:roi_x2]

    # Create a copy of the original image to paste the ROI onto
    pasted_img = img_rgb.copy()

    # 2. Paste (Overlay ROI onto a different position)
    # Let's paste it near the top-left corner (0, 0)
    # We match the size of the cropped ROI to the destination slice
    roi_h, roi_w, _ = roi.shape
    pasted_img[0:roi_h, 0:roi_w] = roi

    # Draw a bounding box on a copy of the original image to show where we cropped from
    marked_original = img_rgb.copy()
    cv2.rectangle(marked_original, (roi_x1, roi_y1), (roi_x2, roi_y2), (255, 0, 0), max(5, int(w * 0.005)))

    # Display the results
    fig, axes = plt.subplots(1, 3, figsize=(18, 6))

    axes[0].imshow(marked_original)
    axes[0].set_title("1. Original with ROI Bounding Box (Red)")
    axes[0].axis('off')

    axes[1].imshow(roi)
    axes[1].set_title("2. Cropped ROI")
    axes[1].axis('off')

    axes[2].imshow(pasted_img)
    axes[2].set_title("3. ROI Copied & Pasted to Top-Left")
    axes[2].axis('off')

    plt.tight_layout()
    plt.show()
