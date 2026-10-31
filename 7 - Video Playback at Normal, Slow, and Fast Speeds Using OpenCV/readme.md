import cv2

cap = cv2.VideoCapture("sample.mp4")

if not cap.isOpened():
    print("Could not open sample.mp4")
    exit()

fps = cap.get(cv2.CAP_PROP_FPS)

if fps <= 0:
    fps = 30

delay = max(1, int(1000 / fps))

print("Playing video at normal speed. Press Q to stop.")
while True:
    ret, frame = cap.read()
    if not ret:
        break

    cv2.imshow("Normal Speed", frame)
    if cv2.waitKey(delay) & 0xFF == ord('q'):
        break

cap.set(cv2.CAP_PROP_POS_FRAMES, 0)
print("Playing video in slow motion. Press Q to stop.")

while True:
    ret, frame = cap.read()
    if not ret:
        break

    cv2.imshow("Slow Motion", frame)
    if cv2.waitKey(delay * 3) & 0xFF == ord('q'):
        break

cap.set(cv2.CAP_PROP_POS_FRAMES, 0)
print("Playing video in fast motion. Press Q to stop.")

while True:
    ret, frame = cap.read()
    if not ret:
        break

    cv2.imshow("Fast Motion", frame)
    if cv2.waitKey(max(1, delay // 3)) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
