# 🗣️ Smart Reader for the Visually Impaired

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-4-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![Tesseract](https://img.shields.io/badge/Tesseract-OCR-44791A?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![IEEE Published](https://img.shields.io/badge/Published-IEEE%20ICCCNT%202024-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **Final Year Major Project | ECE, REVA University, Bengaluru**
> Published at IEEE ICCCNT 2024, IIT Mandi · [View on IEEE Xplore](https://ieeexplore.ieee.org/document/10723858)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [System Architecture](#-system-architecture)
- [Hardware Components](#-hardware-components)
- [Software Stack](#-software-stack)
- [How It Works](#-how-it-works)
- [Performance Metrics](#-performance-metrics)
- [Installation & Setup](#-installation--setup)
- [Usage](#-usage)
- [Results & Gallery](#-results--gallery)
- [Limitations](#-limitations)
- [Future Enhancements](#-future-enhancements)
- [Research Publication](#-research-publication)
- [Contributors](#-contributors)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

---

## 🌟 Overview

**Smart Reader for the Visually Impaired** is an assistive technology device that empowers visually impaired individuals with independent reading capabilities. Built on a Raspberry Pi platform, it converts printed text into real-time audible speech using Optical Character Recognition (OCR) and Text-to-Speech (TTS) technologies.

This project addresses the need for an affordable, portable, and accessible reading device — enabling users to engage with printed material independently, without sighted assistance.

### 🎯 Project Context

| Detail | Info |
|--------|------|
| **Type** | Final Year Major Project |
| **Department** | Electronics & Communication Engineering (ECE) |
| **Institution** | REVA University, Bengaluru, India |
| **Publication** | IEEE ICCCNT Conference 2024, IIT Mandi |
| **DOI** | [10.1109/ICCCNT61001.2024.10723858](https://ieeexplore.ieee.org/document/10723858) |

---

## ✨ Features

- 🔍 **Real-Time Text Recognition** — 97.13% OCR accuracy tested on 100+ samples
- 🔘 **One-Button Operation** — Simple push-button interface for ease of use
- 🔊 **Audio Feedback** — Clear speech output via Bluetooth speaker
- ⚡ **Fast Processing** — ~1.1 seconds per image (capture to audio)
- 📦 **Portable Design** — Compact, self-contained unit in a custom enclosure
- 💰 **Low Cost** — Built with off-the-shelf components
- ♿ **Purpose-Built** — Specifically designed for visually impaired users

---

## 🏗️ System Architecture

The Smart Reader follows a streamlined pipeline:

```
User Input (Button Press) → Image Capture → Preprocessing → OCR → TTS → Audio Output
```

### Hardware Architecture

```
┌─────────────────────┐
│   Push Button       │
│   (GPIO17)          │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐      ┌─────────────────────┐
│  Raspberry Pi 4     │◄────►│  Logitech C270      │
│  Model B            │      │  HD Webcam          │
└──────┬──────────────┘      └─────────────────────┘
       │
       ▼
┌─────────────────────┐
│  Bluetooth Speaker  │
│  (Audio Output)     │
└─────────────────────┘
```

### Software Pipeline

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│    Camera    │───►│   OpenCV     │───►│  Tesseract   │───►│   Festival   │
│   Capture   │    │  Processing  │    │     OCR      │    │     TTS      │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
                          │                    │                    │
                          ▼                    ▼                    ▼
                   Grayscale/Blur      Text Extraction      Audio Generation
```

---

## 🔧 Hardware Components

| Component | Specification | Purpose |
|-----------|--------------|---------|
| **Microprocessor** | Raspberry Pi 4 Model B (8GB RAM) | Main processing unit |
| **Camera** | Logitech C270 HD Webcam (720p) | Image capture |
| **Input Interface** | Metal LED Push Button | User trigger mechanism |
| **Audio Output** | Bluetooth Speaker | Text-to-speech playback |
| **Power Supply** | 5V/3A USB-C Adapter | System power |
| **GPIO Connection** | GPIO17 with Pull-up Resistor | Button interface |
| **Enclosure** | Custom 3D-printed housing | Device protection |

---

## 💻 Software Stack

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **OS** | Raspberry Pi OS | Bullseye | Linux base |
| **Language** | Python | 3.9+ | Core logic |
| **Vision** | OpenCV | 4.x | Image preprocessing |
| **OCR** | Pytesseract | 0.3.x | Text extraction |
| **TTS** | Festival | 2.5 | Speech synthesis |
| **GPIO** | RPi.GPIO | 0.7.x | Hardware control |
| **Imaging** | PIL/Pillow | 9.x | Image handling |

### Key Python Libraries

```python
import cv2                  # Image processing
import pytesseract          # OCR functionality
import RPi.GPIO as GPIO     # Hardware control
import subprocess           # TTS execution
from PIL import Image       # Image handling
```

---

## ⚙️ How It Works

### Step-by-Step Process

1. **Initialization** — System boots, GPIO configured, camera tested
2. **User Interaction** — User places printed material under the camera and presses the button
3. **Image Acquisition** — Webcam captures a high-resolution image
4. **Preprocessing (OpenCV)** — Grayscale conversion → Gaussian blur → Contrast enhancement → Thresholding
5. **Text Extraction (Tesseract)** — OCR processes the image and extracts text
6. **Speech Synthesis (Festival)** — Extracted text is converted to audio and played via speaker
7. **Ready State** — System loops back and waits for the next button press

---

## 📊 Performance Metrics

| Metric | Value |
|--------|-------|
| **Average OCR Accuracy** | 97.13% |
| **Processing Time** | ~1.1 seconds per image |
| **Optimal Font Size** | 10pt – 14pt |
| **Language** | English (primary) |
| **Test Samples** | 100+ |

---

## 🚀 Installation & Setup

### Prerequisites

- Raspberry Pi 4 Model B (2GB+ RAM)
- Raspberry Pi OS (Bullseye or later)
- Internet connection for initial setup
- All hardware components assembled

### Step 1 — Update System

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Step 2 — Install Dependencies

```bash
# Tesseract OCR
sudo apt-get install tesseract-ocr -y

# Festival TTS
sudo apt-get install festival -y

# Python tools
sudo apt-get install python3-pip python3-opencv -y

# Python libraries
pip3 install pytesseract RPi.GPIO pillow
```

### Step 3 — Enable Camera

```bash
sudo raspi-config
# Interface Options → Camera → Enable
```

### Step 4 — GPIO Setup

```python
import RPi.GPIO as GPIO

BUTTON_PIN = 17
GPIO.setmode(GPIO.BCM)
GPIO.setup(BUTTON_PIN, GPIO.IN, pull_up_down=GPIO.PUD_UP)
```

### Step 5 — Bluetooth Speaker

```bash
sudo apt-get install bluetooth bluez bluealsa -y

bluetoothctl
# > power on
# > agent on
# > scan on
# > pair [MAC_ADDRESS]
# > connect [MAC_ADDRESS]
```

### Step 6 — Hardware Assembly

1. Connect push button to GPIO17 and GND
2. Plug USB webcam into Raspberry Pi
3. Pair and connect Bluetooth speaker
4. Attach 5V power supply
5. Mount components in enclosure

---

## 📖 Usage

```bash
cd ~/smart-reader
python3 smart_reader.py
```

### Basic Operation

1. **Power On** — Connect power supply
2. **Wait** — System initializes (~30 seconds)
3. **Position** — Place printed material under camera
4. **Press Button** — Triggers image capture
5. **Listen** — Device reads the text aloud

### Core Code

```python
#!/usr/bin/env python3
import cv2
import pytesseract
import RPi.GPIO as GPIO
import subprocess
from time import sleep

BUTTON_PIN = 17
GPIO.setmode(GPIO.BCM)
GPIO.setup(BUTTON_PIN, GPIO.IN, pull_up_down=GPIO.PUD_UP)

def capture_image():
    cap = cv2.VideoCapture(0)
    ret, frame = cap.read()
    cap.release()
    return frame

def preprocess_image(image):
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    blur = cv2.GaussianBlur(gray, (5, 5), 0)
    return blur

def extract_text(image):
    return pytesseract.image_to_string(image)

def text_to_speech(text):
    subprocess.call(['festival', '--tts'], input=text.encode())

def main():
    print("Smart Reader ready. Press button to scan.")
    try:
        while True:
            if GPIO.input(BUTTON_PIN) == GPIO.LOW:
                print("Capturing...")
                image = capture_image()
                processed = preprocess_image(image)
                text = extract_text(processed)
                print(f"Detected: {text}")
                text_to_speech(text)
                sleep(1)
    except KeyboardInterrupt:
        GPIO.cleanup()

if __name__ == "__main__":
    main()
```

---

## 📸 Results & Gallery

| Visual | Description |
|--------|-------------|
| `Final.jpg` | Fully assembled Smart Reader prototype |
| `Hardware_Architecture.jpg` | Component interconnection diagram |
| `Flowdiagram.png` | End-to-end process flow |
| `Picture_taken.png` | Real-time OCR capture demo |
| `Average.png` | Accuracy and speed analysis chart |
| `Connections.png` | GPIO and peripheral wiring guide |

---

## ⚠️ Limitations

- Handwritten / cursive text has reduced accuracy
- Font sizes below 10pt may not be reliably recognized
- English-only OCR in current version
- Performance degrades in poor lighting
- Reflective surfaces and page curvature can affect results
- Multi-column and artistic layouts may cause errors

---

## 🔮 Future Enhancements

- **Deep Learning OCR** — Improved accuracy for complex fonts and handwriting
- **Multilingual Support** — Regional Indian languages and 10+ major languages
- **Object Detection** — Scene description and currency recognition
- **Hardware Upgrades** — Auto-focus camera, rechargeable battery, haptic feedback
- **AI Integration** — Document summarization and context-aware reading
- **Mobile App** — Android/iOS companion app
- **Voice Commands** — Hands-free operation
- **Braille Output** — Hardware braille display integration

---

## 📚 Research Publication

**Title**: Smart Reader / SpeakEasy Reader — OCR-Based Assistive Device for Visually Impaired  
**Conference**: 15th IEEE International Conference on Computing, Communication and Networking Technologies (ICCCNT 2024)  
**Venue**: IIT Mandi, India  
**DOI**: [10.1109/ICCCNT61001.2024.10723858](https://ieeexplore.ieee.org/document/10723858)

### BibTeX Citation

```bibtex
@inproceedings{harsha2024smartreader,
  title     = {Smart Reader: OCR-Based Assistive Device for Visually Impaired},
  author    = {Harsha, Kuragayala Sree and Naik, Shivani Guru and Tauseef, Md},
  booktitle = {2024 15th International Conference on Computing Communication
               and Networking Technologies (ICCCNT)},
  year      = {2024},
  organization = {IEEE},
  doi       = {10.1109/ICCCNT61001.2024.10723858}
}
```

---

## 👥 Contributors

| Name | Role |
|------|------|
| **Kuragayala Sree Harsha** | Hardware architecture, OCR/TTS pipeline, Raspberry Pi integration, GPIO programming, performance optimization, 3D enclosure design |
| **Shivani Guru Naik** | Software development and testing, user interface design, hardware assembly, documentation, research, system deployment |
| **Md Tauseef** | Component testing and validation, system deployment support |

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- **REVA University, Bengaluru** — For resources and academic support
- **Department of ECE** — For project guidance and mentorship
- **IEEE ICCCNT 2024 Committee** — For accepting our research
- **IIT Mandi** — For hosting the conference
- **OpenCV, Tesseract, Festival** — Open-source tools that made this possible
- **Raspberry Pi Foundation** — For an accessible computing platform
- **Our test users** — Visually impaired individuals who gave invaluable feedback

---

## 📞 Contact

**Shivani Guru Naik**  
🎓 REVA University, Bengaluru | ECE Department  
🔬 Co-author, IEEE ICCCNT 2024

---

**Made with ❤️ for the visually impaired community**

![Built with Raspberry Pi](https://img.shields.io/badge/Built%20with-Raspberry%20Pi-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white)
![Powered by Python](https://img.shields.io/badge/Powered%20by-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![IEEE Published](https://img.shields.io/badge/Published-IEEE-00629B?style=for-the-badge)
