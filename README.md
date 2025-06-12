# 🚘 Automatic License Plate Detection Project (ANPR)

![License Plate Recognition](examples/ANPR.webp)

## Overview

This project is a **real-time parking management system** that leverages **deep learning** and **OCR** to detect and recognize vehicle license plates. It supports **RTSP streams** from IP cameras or local webcam feeds, and logs **entry/exit times** in an SQLite database.

> Developed by **Mohammed Rhellab** **Youness Farhat** **Abdelmohaimen Malhabi** **Dia Alassan** and his team at ISGA Marrakech as part of an academic project.

## Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [System Architecture](#system-architecture)
- [Live Streaming and Detection](#live-streaming-and-detection)
- [Database Integration](#database-integration)
- [Example Outputs](#example-outputs)
- [How It Works](#how-it-works)
- [Future Work](#future-work)
- [License](#license)
- [Contact](#contact)

## ✅ Features

- 📸 **Real-time Detection** from IP camera or webcam  
- 🔤 **OCR Recognition** using EasyOCR  
- 🧠 **YOLOv8 Detection** for high-accuracy plate detection  
- 🗃️ **SQLite Database Logging** for entry/exit time  
- 🧹 **Duplicate Filtering** within short intervals  
- ✅ **Regex Validation** for correct plate format

## 🛠️ Technologies Used

- **YOLOv8** – Deep learning object detector (Ultralytics)
- **EasyOCR** – Optical character recognition engine
- **OpenCV** – Video stream handling & frame capture
- **SQLite** – Lightweight database for logs
- **Python** – Main programming language
- **Regex** – Plate format validation
- **PyTorch** – YOLOv8 backend framework
- **RTSP** – Protocol for IP camera streaming

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/automatic-plate-detection-anpr.git
cd automatic-plate-detection-anpr
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

Ensure you have Python 3.7+ and a camera device or RTSP URL available.

### 3. Database Setup

Create a basic SQLite database:

```sql
CREATE TABLE parking_records (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    license_plate TEXT NOT NULL,
    entry_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    exit_time TIMESTAMP
);
```

Edit `config.py` with your database path:

```python
DATABASE_URI = 'sqlite:///parking.db'
```

## 🧩 System Architecture

```plaintext
[Camera/RTSP] --> [YOLOv8 Detection] --> [EasyOCR] --> [Validation] --> [Database Logging]
       |                                                                 |
       +---------------------------> [Live UI Display] <----------------+
```

## 🎥 Live Streaming and Detection

### RTSP Stream

```bash
python live_detect.py --rtsp-url rtsp://username:password@camera_ip:port --conf-thres 0.5 --iou-thres 0.4
```

### Local Webcam

```bash
python live_detect.py --use-local-camera --conf-thres 0.5 --iou-thres 0.4
```

## 🗄️ Database Integration

Records are automatically managed based on detection:

```sql
CREATE TABLE parking_records (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    license_plate TEXT NOT NULL,
    entry_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    exit_time TIMESTAMP
);
```

Sample Output:

| ID  | License Plate | Entry Time          | Exit Time          |
|-----|---------------|---------------------|--------------------|
| 1   | ABC1234       | 2025-06-01 08:00:00 | 2025-06-01 10:30:00|
| 2   | XYZ5678       | 2025-06-01 08:30:00 |                    |

## 📊 Example Outputs

### Plate Detection

![Car Image](examples/example2.jpg)

### Live Detection Feed

![Live Detection](examples/live_cam_ss.png)

### Database Table

![Database Entry](examples/database.png)

## 🔄 How It Works

### 1. Frame Capture  
Captures from RTSP/local camera.

### 2. Detection  
YOLOv8 locates license plates in the frame.

### 3. OCR  
EasyOCR reads the characters inside the plate bounding box.

### 4. Validation  
Regex filters valid plate formats (customizable).

### 5. Logging  
SQLite stores timestamps for entry and exit.

## 📈 Future Work

- 💳 Payment system integration  
- 📡 Cloud-based remote access  
- 📈 Parking space analytics & heatmaps  
- 🖥️ GUI with dashboard for record viewing  
- 📷 Multi-camera support

## 🪪 License

This project is licensed under the [MIT License](LICENSE).

## 👨‍💻 Contact

Developed by:

- **Name:** Mohammed Rhellab  
- **School:** ISGA Marrakech – Ingénierie des Systèmes Informatiques  
- **GitHub:** [github.com/yourusername](https://github.com/Sparta04)  
- **Email:** medrhe191@gmail.com

---

> _For inquiries or collaboration opportunities, feel free to reach out via GitHub or email._
