# Form Correctness Pose Estimation – Bicep Curl Analysis
This project performs pose detection and form evaluation using MediaPipe Pose and OpenCV.  
It analyses a bicep curl video frame-by-frame, computes elbow and back angles, smooths noisy values, 
applies rule-based posture assessment, and provides real-time feedback overlaid on the video.

---

## Working:

uses **MediaPipe Pose** to detect keypoints:
- Shoulder
- Elbow
- Wrist
- Hip

Once detected, each frame contains X and Y coordinates for joints.

Example:
shoulder = (lm[RIGHT_SHOULDER].x * width, lm[RIGHT_SHOULDER].y * height)

---

## 🔍 How Form Evaluation Works

### 1. Angle Calculation  
Using three joints (A, B, C), elbow and back angles are computed using the cosine rule.

### 2. Angle Smoothing  
A moving window removes jitter:
AngleSmoother → returns an averaged angle for better stability.

### 3. Posture Rules  

- If elbow angle < 40° → "Elbow and Curl flexed too tight"
- If elbow angle > 170° → "Over-flexion elbow"
- If back angle < 160° → "Keep hip stable"
- If no rule is violated → "Good form"

### 4. Wrist angle
- the wrist should stay neutral and aligned with the elbow
- Any upward or downward bend indicates poor form.
-  I detect this by measuring wrist–elbow alignment and warn the user if the wrist 
deviates beyond a safe threshold.

### 4. Rep Counting  
A rep is counted when:
- Arm moves from extended ( >150° ) → downward  
- Then curls up (<80°)

---

## ▶️ How to Run

1. Install libraries:
 !pip install mediapipe opencv-python numpy

3. Add your input video into import files.

4. Run:
   analyse_bicep_curl.py

5. Output video will appear in:
   Analysed_Bicep_Curl.mp4

---

## Structure

- Pose detection using MediaPipe  
- Angle extraction and smoothing  
- Rule-based evaluation  
- Repetition counting  
- Video overlay output   

