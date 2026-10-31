# Step 1: Import required libraries
import cv2
import matplotlib.pyplot as plt
from google.colab import files

# Step 2: Upload an image
uploaded = files.upload()

# Get the uploaded image name
image_name = next(iter(uploaded))

# Step 3: Read the image
image = cv2.imread(image_name)

# Step 4: Convert BGR image to RGB for displaying
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Step 5: Convert image to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Step 6: Apply Canny Edge Detection
edges = cv2.Canny(gray, 100, 200)

# Step 7: Display the results
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(image_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(edges, cmap="gray")
plt.title("Canny Edge / Outline")
plt.axis("off")

plt.show()
