import cv2

# Read the image
image = cv2.imread("sample.jpg")

# Resize the image for display
image = cv2.resize(image, (800, 600))

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Display the images
cv2.imshow("Original Image", image)
cv2.imshow("Grayscale Image", gray_image)

cv2.waitKey(0)
cv2.destroyAllWindows()
