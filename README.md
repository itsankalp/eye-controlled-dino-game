
# 🦖 Eye-Controlled Dino Game

Control the Chrome Dino Game with your **eye blinks** — no keyboard needed.  
This project uses real-time blink detection via webcam to simulate the spacebar press.

![Made by Sankalp Mirajkar](https://img.shields.io/badge/made%20by-Sankalp%20Mirajkar-blue)
![Python](https://img.shields.io/badge/python-3.8+-yellow)
![OpenCV](https://img.shields.io/badge/computer%20vision-OpenCV-red)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 👀 How It Works

- Uses **Dlib** to detect facial landmarks (eyes).
- Calculates **Eye Aspect Ratio (EAR)** to determine when you blink.
- When a blink is detected, it simulates a **spacebar press** using `keyboard` module.
- Works on **chrome://dino** page.

---

## 🎮 How to Use

1. Install requirements:
   ```bash
   pip install -r requirements.txt

   Download the shape_predictor_68_face_landmarks.dat and place it in the same folder.

Add your ChromeDriver path in config.json:

json
Copy
Edit
{
  "driver_path": "C:\\path\\to\\chromedriver.exe"
}
Run the script:

bash
Copy
Edit
python main.py
Go to chrome://dino in your browser and blink to jump!



