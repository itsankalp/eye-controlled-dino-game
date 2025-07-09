# 🦖 Blink-Controlled Dino Game using Dlib
# ✨ Built by Sankalp Mirajkar

import json
import time
import keyboard
import cv2
import dlib
import numpy as np
from scipy.spatial import distance as dist
from selenium import webdriver

class TRex:
    """
    Blink-controlled Dino Game
    Developed by: Sankalp Mirajkar
    """

    def __init__(self, data):
        """Initialize Chrome driver"""
        self.driver = webdriver.Chrome(data['driver_path'])

    def open_game(self):
        """Open Google homepage to start the Dino game"""
        self.driver.get("https://www.google.com")

    def eye_aspect_ratio(self, eye):
        """Calculate Eye Aspect Ratio (EAR)"""
        A = dist.euclidean(eye[1], eye[5])
        B = dist.euclidean(eye[2], eye[4])
        C = dist.euclidean(eye[0], eye[3])
        ear = (A + B) / (2.0 * C)
        return ear

    def play(self):
        """Start the blink detection and play the game"""

        # Facial landmarks for left and right eye
        RIGHT_EYE_POINTS = list(range(36, 42))
        LEFT_EYE_POINTS = list(range(42, 48))

        # EAR threshold and frame counter
        EYE_AR_THRESH = 0.22
        EYE_AR_CONSEC_FRAMES = 3

        COUNTER = 0
        TOTAL = 0

        # Load face detector and predictor
        detector = dlib.get_frontal_face_detector()
        predictor = dlib.shape_predictor('shape_predictor_68_face_landmarks.dat')

        # Start webcam
        cap = cv2.VideoCapture(0)

        while True:
            ret, frame = cap.read()
            if not ret:
                break

            frame = cv2.flip(frame, 1)
            gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
            rects = detector(gray, 0)

            for rect in rects:
                landmarks = np.matrix([[p.x, p.y] for p in predictor(frame, rect).parts()])

                left_eye = landmarks[LEFT_EYE_POINTS]
                right_eye = landmarks[RIGHT_EYE_POINTS]

                # Compute EAR
                ear_left = self.eye_aspect_ratio(left_eye)
                ear_right = self.eye_aspect_ratio(right_eye)
                ear_avg = (ear_left + ear_right) / 2.0

                # Blink detection
                if ear_avg < EYE_AR_THRESH:
                    COUNTER += 1
                else:
                    if COUNTER >= EYE_AR_CONSEC_FRAMES:
                        TOTAL += 1
                        keyboard.press_and_release('space')  # Jump!
                        print("Blink detected - JUMP")
                    COUNTER = 0

                cv2.putText(frame, f"Blinks: {TOTAL}", (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0, 0, 255), 2)

            cv2.imshow("Blink Detection - Sankalp's Dino", frame)

            if cv2.waitKey(1) & 0xFF == ord('q'):
                break

        cap.release()
        cv2.destroyAllWindows()

# ------------ Main ------------
if __name__ == "__main__":
    with open('config.json') as config_file:
        data = json.load(config_file)

    game = TRex(data)
    game.open_game()
    time.sleep(1)
    game.play()
