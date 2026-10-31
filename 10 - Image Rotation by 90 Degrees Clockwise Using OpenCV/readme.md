import cv2

image = cv2.imread("sample.jpg")

if image is None:
    print("Image not found!")
    exit()

image = cv2.resize(image, (800, 600))

rotated_image = cv2.rotate(
    image, cv2.ROTATE_90_CLOCKWISE
)

cv2.imshow("Original Image", image)
cv2.imshow("Rotated Image - 90 Degrees Clockwise", rotated_image)

cv2.waitKey(0)
cv2.destroyAllWindows()
