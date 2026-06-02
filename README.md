# 🏥 Healthcare Patient Monitor
### Real-time AI Patient Monitoring System using Emotion Detection, Gesture Recognition & Voice Alerts

> A deep learning system that monitors patients in real-time by detecting facial emotions, recognising hand gestures, and automatically triggering **voice alerts** when distress is detected — designed for healthcare and assisted care environments.

---

## 🔍 Project Overview

This system combines **CNN-based emotion recognition**, **MediaPipe gesture detection**, and **automated voice alerts** to monitor patient wellbeing without constant human supervision.

When a patient shows sustained distress or makes an emergency gesture, the system:
- 🔴 Displays a visual alert banner on screen
- 🔊 **Speaks the alert aloud** — *"Warning. Patient showing sustained distress. Please check on them."*
- 📟 Triggers nurse call notification

---

## 🎯 Key Features

| Feature | Description |
|---|---|
| 😊 **7-Class Emotion Detection** | Angry, Disgust, Fear, Happy, Sad, Surprise, Neutral |
| 🤚 **Hand Gesture Recognition** | HELP, STOP, OK, THUMBS UP |
| 🚨 **Voice Alert System** | Automated speech alerts via PowerShell TTS |
| 📊 **Sustained Distress Detection** | Monitors 60-frame rolling buffer — alerts if >60% distress |
| 🧬 **Face Mesh Landmarks** | 468-point facial mesh via MediaPipe |
| ⏱️ **Alert Cooldown** | 10-second cooldown prevents alert flooding |

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat-square&logo=keras&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-0097A7?style=flat-square&logo=google&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)

---

## 📁 Project Structure

```
healthcare-patient-monitor/
│
├── healthcare.ipynb       # Full pipeline — training + real-time monitor
├── emotion_model.h5       # Trained CNN emotion model
└── README.md
```

---

## 🔄 How It Works

### 1. Emotion Detection (CNN)
- Trained on **FER2013 Dataset** — [Available on Kaggle](https://www.kaggle.com/datasets/msambare/fer2013)
- **7 emotion classes:** Angry, Disgust, Fear, Happy, Sad, Surprise, Neutral
- Input: 48×48 grayscale face images
- Architecture: 3× Conv2D + MaxPooling → Dense(256) → Dropout(0.4) → Softmax(7)
- Alert emotions: **Angry, Fear, Sad**

### 2. Gesture Recognition (MediaPipe)
- Detects hand landmarks in real-time
- Recognises 4 gestures:

| Gesture | Trigger |
|---|---|
| ✊ Fist | **HELP** — Emergency alert |
| 🖐️ Open hand | STOP |
| 👍 Thumb up | THUMBS UP |
| 👌 OK sign | OK |

### 3. Sustained Distress Detection
- Tracks last **60 frames** using a rolling buffer
- If **>60% of frames** show distress emotions → triggers nurse alert

### 4. Voice Alert System
- Uses **Windows PowerShell TTS** (Text-to-Speech)
- 10-second cooldown between alerts
- Two alert types:
  - *"Patient showing sustained distress — please check on them"*
  - *"Emergency! Patient needs help — call the nurse immediately"*

---

## ▶️ How to Run

```bash
# Install dependencies
pip install tensorflow opencv-python mediapipe numpy

# Run the notebook
jupyter notebook healthcare.ipynb
```

> ⚠️ Voice alerts use Windows PowerShell TTS — works on Windows only.  
> Dataset: Download FER2013 from [Kaggle](https://www.kaggle.com/datasets/msambare/fer2013) and place in `archive/train` and `archive/test` folders.

---

## 🚨 Alert System Flow

```
Camera Feed
    │
    ├── Face Detected → CNN Emotion → Distress? → Rolling Buffer
    │                                                    │
    │                                              60% distress?
    │                                                    │
    └── Hand Detected → Gesture → HELP gesture?   → VOICE ALERT 🔊
                                        │               │
                                        └───────────────┘
                                          CALL NURSE BANNER
```

---

## 👩‍💻 Author

**Aleena Elizabeth Thomas**  
[LinkedIn](https://linkedin.com/in/aleena-elizabeth-thomas) · [GitHub](https://github.com/aleenaelizabethth)
