# granny-cam

This code implements a **motion detection system** using **OpenCV** and plays an alert sound when significant motion is detected. Here's how it works:

---

### **Functionality**

1. **Video Feed**:
   - Captures video using `cv2.VideoCapture(1)`, which accesses the second connected camera (index `1`).
   - Reads two consecutive frames (`frame1` and `frame2`) to detect changes (motion).

2. **Motion Detection**:
   - Computes the **absolute difference** between two consecutive frames using `cv2.absdiff(frame1, frame2)`.
   - Converts the difference frame to grayscale using `cv2.cvtColor`.
   - Applies Gaussian blur with a kernel size of `(5, 5)` to reduce noise.
   - Thresholds the blurred image to create a binary image (`cv2.threshold`) for highlighting motion areas.
   - Dilates the binary image to fill gaps and make contours more distinct (`cv2.dilate`).

3. **Contour Detection**:
   - Finds contours in the dilated binary image (`cv2.findContours`).
   - Filters out small contours by checking their area (`cv2.contourArea`).

4. **Alert Mechanism**:
   - For contours with an area greater than `5000`, the script:
     - Draws a green rectangle around the motion area using `cv2.rectangle`.
     - Plays an alert sound (`alert.wav`) asynchronously using `winsound.PlaySound`.

5. **Exit Condition**:
   - The program stops if the **'q'** key is pressed (`cv2.waitKey(10)`).

6. **Output**:
   - Displays the live feed with detected motion highlighted as green rectangles in a window titled `'Granny Cam'`.

---

### **Features**
- **Motion Detection**:
  - Highlights significant motion in the video feed by drawing bounding rectangles.
- **Sound Alert**:
  - Plays an audio alert (`alert.wav`) whenever motion is detected.

---

### **Dependencies**
- **OpenCV**: For video capture and image processing.
- **NumPy**: For handling arrays (implicitly used by OpenCV).
- **winsound**: For playing sound alerts on Windows.

---

### **Possible Improvements**
1. **Sensitivity Adjustment**:
   - Adjust the `5000` area threshold to fine-tune the motion sensitivity.
   - Add a GUI slider or configuration file for dynamic control.

2. **Multi-Platform Sound Support**:
   - Replace `winsound` (Windows-only) with a cross-platform library like **playsound** or **pydub**.

3. **Save Intrusion Footage**:
   - Save frames or video clips when motion is detected for later review.

4. **HTTP Notification**:
   - Use the `requests` library to send alerts or snapshots to a server or email (currently imported but unused).

5. **Frame Stabilization**:
   - Add preprocessing to handle small camera jitters, which can trigger false motion detection.

6. **Exit Gracefully**:
   - Release the camera (`cam.release()`) and destroy windows (`cv2.destroyAllWindows()`) when exiting.
