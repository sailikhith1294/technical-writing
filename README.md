# Face and Eye Detection in Python using OpenCV 👀

This tutorial demonstrates how to build a simple face and eye detector using Python and OpenCV. It’s beginner-friendly and great for anyone getting started with computer vision.


## 🔧 Requirements
Make sure you have Python installed. Then install OpenCV:

bash
pip install opencv-python

OpenCV uses pre-trained Haar Cascade classifiers to detect objects in images and video. We'll use:
haarcascade_frontalface_default.xml – for face detection
haarcascade_eye.xml – for eye detection

import cv2

# Load the cascade classifiers
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')
eye_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_eye.xml')

# Start video capture
cap = cv2.VideoCapture(0)

while True:
    # Read a frame
    ret, frame = cap.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    
    # Detect faces
    faces = face_cascade.detectMultiScale(gray, 1.3, 5)
    
    for (x, y, w, h) in faces:
        # Draw rectangle around face
        cv2.rectangle(frame, (x, y), (x+w, y+h), (255, 0, 0), 2)
        roi_gray = gray[y:y+h, x:x+w]
        roi_color = frame[y:y+h, x:x+w]
        
        # Detect eyes within the face
        eyes = eye_cascade.detectMultiScale(roi_gray)
        for (ex, ey, ew, eh) in eyes:
            cv2.rectangle(roi_color, (ex, ey), (ex+ew, ey+eh), (0, 255, 0), 2)

    # Show the result
    cv2.imshow('Face and Eye Detector', frame)

    # Exit with 'q'
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()


✅ Output
Once you run this script, it will open your webcam and draw:
🔵 Blue rectangles around detected faces
🟢 Green rectangles around detected eyes

📌 Notes
Make sure your webcam is connected.
The model works best in well-lit environments.
Press Q to quit the window.

🙌 Credits
This project uses OpenCV’s built-in Haar Cascade models.

📁 License
Feel free to use or modify this for learning or demo purposes.

