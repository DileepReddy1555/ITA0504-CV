import cv2
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
uploaded = files.upload()

# Read image
image_path = list(uploaded.keys())[0]
img = cv2.imread(image_path)

# Rotate image 270 degrees clockwise
rotated_img = cv2.rotate(img, cv2.ROTATE_90_COUNTERCLOCKWISE)

# Display original and rotated images
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(rotated_img, cv2.COLOR_BGR2RGB))
plt.title("270 Degree Clockwise Rotated Image")
plt.axis("off")

plt.show()

# Save rotated image
cv2.imwrite("rotated_270_image.jpg", rotated_img)

# Download output
files.download("rotated_270_image.jpg")
