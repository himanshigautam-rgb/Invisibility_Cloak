import cv2
import numpy as np
import time
import matplotlib.pyplot as plt

# Start webcam (0 = default camera)
cap = cv2.VideoCapture(0)

# Check if the webcam is opened
if not cap.isOpened():
    print("Error: Could not access the webcam.")
    exit()

# Give the camera some time to warm up
print("Warming up the camera...")
time.sleep(3)

# Capture background (still scene without cloak)
print("Capturing background...")
for i in range(30):
    ret, background = cap.read()
    if not ret:
        print("Warning: Could not read frame from webcam.")
        continue
background = np.flip(background, axis=1)
print("Background captured successfully.")

# Set up matplotlib for real-time display
plt.ion()
fig, ax = plt.subplots()
img_display = ax.imshow(np.zeros_like(background))  # Placeholder for the first frame
plt.title("Invisibility Cloak - Live")
plt.axis('off')

try:
    while True:
        ret, frame = cap.read()
        if not ret:
            print("Error: Could not read frame from webcam.")
            break

        frame = np.flip(frame, axis=1)
        hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

        # Define color range for the cloak (e.g., red)
        lower_red1 = np.array([0, 120, 70])
        upper_red1 = np.array([10, 255, 255])
        lower_red2 = np.array([170, 120, 70])
        upper_red2 = np.array([180, 255, 255])

        # Create mask to detect red color
        mask1 = cv2.inRange(hsv, lower_red1, upper_red1)
        mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
        mask = mask1 + mask2

        # Clean the mask
        mask = cv2.morphologyEx(mask, cv2.MORPH_OPEN, np.ones((3, 3), np.uint8))
        mask = cv2.morphologyEx(mask, cv2.MORPH_DILATE, np.ones((3, 3), np.uint8))

        # Replace red cloak with background
        cloak_area = cv2.bitwise_and(background, background, mask=mask)
        inverse_mask = cv2.bitwise_not(mask)
        non_cloak_area = cv2.bitwise_and(frame, frame, mask=inverse_mask)

        # Combine both parts
        final_output = cv2.addWeighted(cloak_area, 1, non_cloak_area, 1, 0)

        # Update the matplotlib display
        img_display.set_data(cv2.cvtColor(final_output, cv2.COLOR_BGR2RGB))
        plt.pause(0.01)  # Pause to update the frame

except KeyboardInterrupt:
    print("Exiting...")

finally:
    
    cap.release()
    plt.close()