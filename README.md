🗣️ Smart Reader for the Visually Impaired
=========================================

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Raspberry%20Pi-4-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white" alt="Raspberry Pi">
  <img src="https://img.shields.io/badge/OpenCV-4.x-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" alt="OpenCV">
  <img src="https://img.shields.io/badge/Tesseract-OCR-4479A1?style=for-the-badge" alt="Tesseract">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Published-IEEE%20ICCCNT%202024-blue?style=for-the-badge" alt="IEEE Published">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge" alt="Status">
</p>

---

## 📋 Table of Contents

- [Overview](#-overview)  
- [Project Context](#-project-context)  
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
- [Contact & Support](#-contact--support)  

---

## 🌟 Overview

Smart Reader for the Visually Impaired is an assistive embedded system designed to give visually impaired users **independent reading capability** by converting printed text into real‑time speech.  
Built on a Raspberry Pi platform, it uses a camera for text capture, OpenCV for preprocessing, Tesseract for OCR, and Festival for text‑to‑speech output.

This project focuses on providing an **affordable, portable, and user‑friendly** alternative to expensive commercial reading devices, enabling visually impaired users to access printed information without constant sighted assistance.

---

## 🎯 Project Context

- **Type:** Final Year Major Project  
- **Department:** Electronics & Communication Engineering (ECE)  
- **Institution:** REVA University, Bengaluru, India  
- **Publication:** IEEE ICCCNT 2024, IIT Mandi  
- **Research Paper:** [View on IEEE Xplore](https://ieeexplore.ieee.org/document/10723858)

---

## ✨ Features

- **Real‑Time Text Recognition:** OCR with average accuracy of **97.13%**  
- **One‑Button Operation:** Simple push‑button GPIO interface for non‑technical users  
- **Audio Feedback:** Clear TTS via Bluetooth speaker  
- **Fast Processing:** ~**1.1 seconds** per image from capture to audio  
- **Portable Design:** Compact and self‑contained with custom enclosure  
- **Low Cost:** Built from easily available, off‑the‑shelf components  
- **Embedded Integration:** Complete hardware‑software system on Raspberry Pi  
- **Assistive Focus:** Designed specifically for visually impaired users

---

## 🏗️ System Architecture

**High‑Level Pipeline**

> User Button Press → Image Capture → Preprocessing → OCR → Text‑to‑Speech → Audio Output

### Hardware Architecture

```text
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

```text
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│    Camera    │───►│   OpenCV     │───►│  Tesseract   │───►│   Festival   │
│   Capture    │    │  Processing  │    │     OCR      │    │     TTS      │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘

       │                    │                    │
       ▼                    ▼                    ▼
Image acquisition    Image enhancement      Text extraction      Audio output
```

---

## 🔧 Hardware Components

| Component            | Specification                         | Purpose                      |
|----------------------|---------------------------------------|------------------------------|
| Microprocessor       | Raspberry Pi 4 Model B (8 GB RAM)     | Main processing unit         |
| Camera               | Logitech C270 HD Webcam (720p)        | Image capture                |
| Input Interface      | Metal LED Push Button (GPIO17)        | User trigger mechanism       |
| Audio Output         | Bluetooth Speaker                     | Text‑to‑speech playback      |
| Power Supply         | 5 V / 3 A USB‑C Adapter               | System power                 |
| GPIO Connection      | GPIO17 with pull‑up resistor          | Button input interface       |
| Enclosure            | Custom 3D‑printed / custom housing    | Mechanical protection, UX    |

---

## 💻 Software Stack

| Layer             | Technology        | Version  | Purpose                     |
|-------------------|-------------------|----------|-----------------------------|
| Operating System  | Raspberry Pi OS   | Bullseye | Base OS                     |
| Programming       | Python            | 3.9+     | Core application logic      |
| Computer Vision   | OpenCV            | 4.x      | Image preprocessing         |
| OCR Engine        | Pytesseract       | 0.3.x    | Text extraction             |
| TTS Engine        | Festival          | 2.5      | Speech synthesis            |
| Hardware Control  | RPi.GPIO          | 0.7.x    | GPIO button handling        |
| Image Processing  | PIL / Pillow      | 9.x      | Image manipulation          |

**Key Python Imports**

```python
import cv2                 # Image processing
import pytesseract         # OCR functionality
import RPi.GPIO as GPIO    # Hardware control
import subprocess          # TTS execution
from PIL import Image      # Image handling
from time import sleep
```

---

## ⚙️ How It Works

### 1. Initialization

- Raspberry Pi boots and loads required libraries  
- GPIO pin configured for the push button  
- Camera initialized and tested  

### 2. User Interaction

- User places printed text under the camera  
- User presses the GPIO push button (GPIO17)  

### 3. Image Acquisition

- Webcam captures a high‑resolution frame  
- Image stored temporarily for processing  

### 4. Preprocessing (OpenCV)

- Convert to grayscale  
- Apply Gaussian blur for noise reduction  
- Enhance contrast  
- Apply thresholding for clearer text regions  

### 5. Text Extraction (Tesseract)

- Preprocessed image sent to Tesseract  
- OCR performs character recognition  
- Extracted text cleaned and formatted  

### 6. Speech Synthesis (Festival)

- Extracted text passed to Festival TTS  
- Audio stream generated  
- Output delivered via Bluetooth speaker  

### 7. Completion

- System returns to ready state  
- Waits for the next button press  

---

## 📊 Performance Metrics

**Accuracy & Speed**

| Metric                 | Value      | Notes                        |
|------------------------|-----------:|------------------------------|
| Average OCR Accuracy   | 97.13%     | Tested on 100+ samples       |
| Processing Time        | ~1.1 s     | Capture → Audio output       |
| Supported Fonts        | High       | Standard printed fonts       |
| Language               | English    | Current implementation       |

**Test Conditions**

- Font Size: 10 pt – 14 pt (optimal)  
- Lighting: Indoor natural/artificial lighting  
- Text Type: Printed documents, books, labels  
- Paper: Standard white / off‑white sheets  

Global WHO data indicates that over **2.2 billion** people live with some form of vision impairment, highlighting the need for practical assistive reading devices like this system.

---

## 🚀 Installation & Setup

### Prerequisites

- Raspberry Pi 4 Model B (2 GB RAM minimum, 4–8 GB recommended)  
- Raspberry Pi OS (Bullseye or later)  
- Internet access for package installation  
- Assembled hardware (Pi, camera, button, speaker, power)  

### 1. Update System Packages

```bash
sudo apt-get update
sudo apt-get upgrade -y
```

### 2. Install Required Dependencies

```bash
# Tesseract OCR
sudo apt-get install tesseract-ocr -y

# Festival TTS
sudo apt-get install festival -y

# Python + OpenCV
sudo apt-get install python3-pip python3-opencv -y

# Python libraries
pip3 install pytesseract RPi.GPIO pillow
```

### 3. Configure Camera

```bash
sudo raspi-config
# Interface Options → Camera → Enable
```

### 4. GPIO Setup (Example)

```python
import RPi.GPIO as GPIO

BUTTON_PIN = 17
GPIO.setmode(GPIO.BCM)
GPIO.setup(BUTTON_PIN, GPIO.IN, pull_up_down=GPIO.PUD_UP)
```

### 5. Bluetooth Speaker Setup

```bash
sudo apt-get install bluetooth bluez bluealsa -y
bluetoothctl
# power on
# agent on
# scan on
# pair [MAC_ADDRESS]
# connect [MAC_ADDRESS]
```

### 6. Hardware Assembly

- Connect push button between GPIO17 and GND (with pull‑up)  
- Connect USB webcam to Raspberry Pi  
- Pair Bluetooth speaker with Raspberry Pi  
- Connect 5 V power supply  
- Place everything into an enclosure (3D‑printed or custom)  

---

## 📖 Usage

### Basic Operation

1. Power on the Raspberry Pi  
2. Wait for system initialization (~30 seconds)  
3. Place printed text under the camera  
4. Press the push button  
5. Listen to the spoken output from the speaker  

### Running the Application

```bash
cd ~/smart-reader
python3 smart_reader.py
```

### Sample Code Structure

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
    text = pytesseract.image_to_string(image)
    return text

def text_to_speech(text):
    subprocess.call(['festival', '--tts'], input=text.encode())

def main():
    print("Smart Reader initialized. Press button to read.")
    try:
        while True:
            if GPIO.input(BUTTON_PIN) == GPIO.LOW:
                print("Button pressed! Capturing image...")
                image = capture_image()
                processed = preprocess_image(image)
                text = extract_text(processed)
                print(f"Text detected: {text}")
                text_to_speech(text)
                sleep(1)
    except KeyboardInterrupt:
        GPIO.cleanup()

if __name__ == "__main__":
    main()
```

---

## 📸 Results & Gallery

_Add the following into a `docs/` or `images/` folder and link here:_

- Final assembled device photos  
- Internal hardware layout  
- System architecture diagram  
- Example screenshots of OCR outputs  
- Demo snapshots (or GIFs) of live usage  

---

## ⚠️ Limitations

- **Handwritten Text:** Limited recognition for cursive or stylized handwriting  
- **Small Fonts:** Accuracy drops for fonts smaller than ~10 pt  
- **Language Support:** Currently optimized for English only  
- **Lighting:** Performance degrades in very low or uneven lighting  
- **Complex Layouts:** Multi‑column or decorative layouts may reduce OCR performance  
- **Image Quality:** Blurry or low‑contrast images lower accuracy  

---

## 🔮 Future Enhancements

- **Deep Learning OCR:** Improve robustness and handwriting support with neural OCR  
- **Multilingual Support:** Add Indian regional languages and auto language detection  
- **Advanced Features:** Object detection, currency recognition, QR/Barcode reading  
- **Hardware Upgrades:** Auto‑focus camera, rechargeable battery, haptic feedback  
- **AI Integration:** Summarization of long documents, context‑aware reading, Q&A  
- **Connectivity:** Companion mobile app and optional cloud processing  
- **Accessibility:** Voice‑command control, digital document (PDF) support, Braille output integration  

---

## 📚 Research Publication

This work is published as a peer‑reviewed paper:

- **Title:** Smart Reader / SpeakEasy Reader — OCR‑Based Assistive Device for Visually Impaired  
- **Conference:** 15th IEEE International Conference on Computing, Communication and Networking Technologies (ICCCNT 2024)  
- **Venue:** IIT Mandi, India  
- **DOI:** [10.1109/ICCCNT61001.2024.10723858](https://ieeexplore.ieee.org/document/10723858)

**Abstract (Short)**  
An affordable, portable OCR‑based reading device for visually impaired users is presented, achieving ~97.13% OCR accuracy and ~1.1 s processing time per page, offering a practical alternative to high‑cost commercial solutions.

**Citation**

```bibtex
@inproceedings{harsha2024smartreader,
  title     = {Smart Reader: OCR-Based Assistive Device for Visually Impaired},
  author    = {Kuragayala Sree Harsha and Shivani Guru Naik and Md Tauseef},
  booktitle = {2024 15th International Conference on Computing, Communication and Networking Technologies (ICCCNT)},
  year      = {2024},
  organization = {IEEE},
  doi       = {10.1109/ICCCNT61001.2024.10723858}
}
```

---

## 👥 Contributors

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/SreeHarshaKuragayala">
        <b>Kuragayala Sree Harsha</b>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/ShivaniGuruNaik">
        <b>Shivani Guru Naik</b>
      </a>
    </td>
    <td align="center">
      <b>Md Tauseef</b>
    </td>
  </tr>
</table>

### Roles & Responsibilities

| Contributor            | Contributions                                                                                 |
|------------------------|-----------------------------------------------------------------------------------------------|
| Kuragayala Sree Harsha| Hardware architecture · OCR & TTS pipeline · Raspberry Pi & GPIO programming · Optimization   |
| Shivani Guru Naik      | Software development & testing · Hardware assembly & integration · Documentation · Co‑author |
| Md Tauseef            | Component testing · Validation · System deployment support                                    |

---

## 📄 License

This project is licensed under the **MIT License**.

```text
MIT License

Copyright (c) 2024
Kuragayala Sree Harsha, Shivani Guru Naik, Md Tauseef

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

[... full MIT license text ...]
```

(Include the full MIT text in your `LICENSE` file as well.)

---

## 🙏 Acknowledgments

- REVA University, Bengaluru – for infrastructure and academic support  
- Department of ECE – for guidance and mentorship  
- IEEE ICCCNT 2024 Committee – for accepting and hosting the work  
- IIT Mandi – conference venue  
- Open‑source communities behind OpenCV, Tesseract, and Festival  
- Raspberry Pi Foundation – for the embedded computing platform  
- Visually impaired users who provided feedback during testing  

---

## 📞 Contact & Support

**Shivani Guru Naik**  
📧 Email: [shivanigurunaik@gmail.com](mailto:shivanigurunaik@gmail.com)  
🐙 GitHub: [github.com/ShivaniGuruNaik](https://github.com/ShivaniGuruNaik)  
🎓 Institution: REVA University, Bengaluru  
🔬 Department: Electronics & Communication Engineering  
📄 IEEE Co‑author: [ICCCNT 2024 Paper](https://ieeexplore.ieee.org/document/10723858)

---

<p align="center">
  <b>Made with ❤️ for the visually impaired community</b><br>
  <sub>Empowering independence through technology</sub>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Built%20with-Raspberry%20Pi-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white" alt="Built with Raspberry Pi">
  <img src="https://img.shields.io/badge/Powered%20by-Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Powered by Python">
  <img src="https://img.shields.io/badge/Published-IEEE-00629B?style=for-the-badge" alt="Published IEEE">
</p>
