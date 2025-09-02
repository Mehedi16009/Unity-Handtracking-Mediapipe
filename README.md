# Unity-Handtracking-Mediapipe
This project demonstrates real-time hand tracking and object interaction in Unity 6.1 (6000 LTS) using a standard laptop/USB webcam and Google MediaPipe Hands.

##👉 Workflow:

Python + MediaPipe detects 21 hand landmarks from your webcam.

Landmarks are streamed to Unity over UDP.

Unity uses the landmark data to recognize gestures (e.g., pinch) and allows you to grab, move, and release 3D objects with physics.

No VR/AR headset is required — just your laptop webcam.
-----
##✨ Features

Hand landmark detection (21 points per hand).

Real-time UDP streaming from Python → Unity.

Simple gesture recognition (Pinch/Fist).

Grabbable 3D objects with physics.

Beginner-friendly setup for macOS M1 (works on Windows/Linux too).
------
##🏗️ System Architecture
```bash 
   [Webcam]
      │
      ▼
+-----------------+         UDP Socket        +------------------+
|  Python Script  |  --------------------->   |   Unity Engine   |
| (MediaPipe)     |                           | (C# Receiver)    |
+-----------------+                           +------------------+
      │                                             │
      ▼                                             ▼
 [Hand Landmarks]                          [3D Object Interaction]



```
------
##📋 Prerequisites
#OS Tested

macOS Sequoia 15.2 (Apple Silicon M1) ✅

Windows 11 (x86_64) ⚠️ (not tested by default, should work)

Ubuntu 22.04+ ⚠️

##Required Installs

1. Unity Hub → Download

     -Install Unity 6000.x LTS (choose latest minor, e.g., 6000.0.23f1).

     -Make sure to install the Mac Build Support module.

2. Git → Download

3. Python 3.10+ (recommended: 3.10.12)

macOS: 
```bash 
brew install python@3.10
```
4. Virtual Environment + Dependencies
   ```bash
   python3 -m venv .venv
source .venv/bin/activate   # (macOS/Linux)
# .venv\Scripts\activate    # (Windows PowerShell)
```
pip install --upgrade pip
pip install mediapipe==0.10.9 opencv-python==4.9.0.80 numpy==1.26.4
```
----
##⚙️ Installation & Setup

3. Unity Side (Receiver + Interaction)

Open Unity Hub → Add project → Select this repo folder → Use Unity 6000.x LTS.

-In Unity, press ▶ Play.

-Unity will open a UDP listener and start receiving landmarks.

-Move your hand in front of the webcam:

-Pinch your fingers → grab the cube/sphere.

-Release → drop with physics.
---
##🧩 File Structure
```bash
unity-handtracking-mediapipe/
│
├── python/
│   ├── hand_tracking_sender.py   # MediaPipe + UDP sender
│   └── requirements.txt          # Python dependencies
│
├── unity/
│   ├── Assets/
│   │   ├── Scripts/
│   │   │   ├── UDPReceiver.cs    # Receives landmarks
│   │   │   ├── HandInteraction.cs # Gesture logic
│   │   │   └── ObjectGrabber.cs  # Object pickup physics
│   │   └── Scenes/
│   │       └── DemoScene.unity
│   └── ProjectSettings/
│
└── README.md

```
------

## 🧪 Testing

✅ Webcam feed opens in Python.

✅ Landmarks stream to Unity (check Console logs).

✅ Unity shows grab state debug (OnGrabStart / OnGrabEnd).

✅ Cube follows pinch gesture.
---
## 🛠️ Troubleshooting

Webcam black screen (macOS) → System Settings → Privacy & Security → Camera → Allow Terminal/Python.

UDP not received → Check firewall → Ensure Python and Unity are on the same port 5005.

Laggy FPS → Reduce webcam resolution in Python (cv2.VideoCapture(0, cv2.CAP_DSHOW) and set .set(3, 640), .set(4, 480)).

Landmark jitter → Add smoothing in Unity (Lerp or Kalman filter).
----
