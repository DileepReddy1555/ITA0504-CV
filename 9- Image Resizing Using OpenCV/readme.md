import cv2

image = cv2.imread("sample.jpg")

if image is None:
    print("Image not found!")
    exit()

image = cv2.resize(image, (800, 600))

small_image = cv2.resize(
    image, None, fx=0.5, fy=0.5
)

big_image = cv2.resize(
    image, None, fx=1.5, fy=1.5
)

cv2.imshow("Original Image", image)
cv2.imshow("Smaller Image", small_image)
cv2.imshow("Bigger Image", big_image)

cv2.waitKey(0)
cv2.destroyAllWindows()
