import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = 'king.jpg'
try:
    # Load original image
    img = cv2.imread(image_path)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    h, w, c = img_rgb.shape

    # Create a separate transparent layer for the watermark
    watermark_layer = np.zeros_like(img_rgb)

    # Define watermark details
    watermark_text = "© COPYRIGHT - PROTECTED"
    font = cv2.FONT_HERSHEY_DUPLEX
    
    # Scale font size dynamically based on image width
    font_scale = w / 1200.0
    thickness = max(1, int(font_scale * 2))
    
    # Get size of the watermark text
    text_size, baseline = cv2.getTextSize(watermark_text, font, font_scale, thickness)
    text_w, text_h = text_size

    # Place watermark in the bottom-right corner with padding
    padding = int(w * 0.03)
    x = w - text_w - padding
    y = h - padding

    # Draw the text on the watermark layer in white
    cv2.putText(watermark_layer, watermark_text, (x, y), font, font_scale, (255, 255, 255), thickness, cv2.LINE_AA)

    # Blend the watermark layer with the original image
    # Alpha is the opacity of the original image, Beta is the opacity of the watermark
    alpha = 1.0
    beta = 0.35  # Adjust transparency of the watermark
    watermarked_img = cv2.addWeighted(img_rgb, alpha, watermark_layer, beta, 0)

    # Display side-by-side comparison
    fig, axes = plt.subplots(1, 2, figsize=(15, 8))
    axes[0].imshow(img_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis('off')

    axes[1].imshow(watermarked_img)
    axes[1].set_title("Watermarked Image (Bottom-Right Corner)")
    axes[1].axis('off')

    plt.tight_layout()
    plt.show()
