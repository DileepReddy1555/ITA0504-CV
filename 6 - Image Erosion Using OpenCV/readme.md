import cv2
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
f = files.upload()
img = cv2.imread(list(f.keys())[0])

# Create kernel
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5,5))
…plt.subplot(1,2,2)
plt.imshow(cv2.cvtColor(eroded, cv2.COLOR_BGR2RGB))
plt.title("Eroded Image")
plt.axis("off")

plt.show()
