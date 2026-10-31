import cv2
import matplotlib.pyplot as plt

def analyze_histogram(image_path):
    image = cv2.imread(image_path)

    if image is None:
        print("Image not found!")
        return

    colors = ("b", "g", "r")
    channel_names = ("Blue", "Green", "Red")

    for i, color in enumerate(colors):
        histogram = cv2.calcHist(
            [image], [i], None, [256], [0, 256]
        )
        plt.plot(histogram, color=color, label=channel_names[i])

    plt.title("Color-Level Histogram")
    plt.xlabel("Pixel Intensity")
    plt.ylabel("Number of Pixels")
    plt.legend()
    plt.show()

analyze_histogram("sample.jpg")
