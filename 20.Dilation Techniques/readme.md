import cv2
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
uploaded = files.upload()

# Read uploaded image
image_path = list(uploaded.keys())[0]
img = cv2.imread(image_path)

# Convert image into grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Define 5x5 kernel
kernel = np.ones((5, 5), np.uint8)

# Apply dilation
dilated_img = cv2.dilate(gray, kernel, iterations=1)

# Display original and dilated images
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plt.imshow(gray, cmap='gray')
plt.title("Original Grayscale Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(dilated_img, cmap='gray')
plt.title("Dilated Image")
plt.axis('off')

plt.show()

# Save output
cv2.imwrite("dilated_image.jpg", dilated_img)

# Download output
files.download("dilated_image.jpg")
