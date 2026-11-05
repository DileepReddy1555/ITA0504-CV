import cv2
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
uploaded = files.upload()

# Read image
image_path = list(uploaded.keys())[0]
img = cv2.imread(image_path)

# Get image dimensions
height, width = img.shape[:2]

# Create 180-degree rotation matrix
center = (width // 2, height // 2)
rotation_matrix = cv2.getRotationMatrix2D(center, 180, 1.0)

# Perform rotation
rotated_img = cv2.warpAffine(img, rotation_matrix, (width, height))

# Display original and rotated images
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(rotated_img, cv2.COLOR_BGR2RGB))
plt.title("180 Degree Rotated Image")
plt.axis("off")

plt.show()

# Save rotated image
cv2.imwrite("rotated_image.jpg", rotated_img)

# Download output
files.download("rotated_image.jpg")
