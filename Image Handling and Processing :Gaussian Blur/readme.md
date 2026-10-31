import cv2

# Read the image
image = cv2.imread("sample.jpg")

# Resize the image for display
image = cv2.resize(image, (800, 600))

# Apply Gaussian Blur
blurred_image = cv2.GaussianBlur(image, (5, 5), 0)

# Display the images
cv2.imshow("Original Image", image)
cv2.imshow("Gaussian Blurred Image", blurred_image)

cv2.waitKey(0)
cv2.destroyAllWindows()
