# 🚗 Vehicle Speed Detection using Computer Vision

A Python-based project that detects vehicles in a video stream and estimates their speed using **Object Tracking** and **Frame-by-Frame Motion Analysis**. This project serves as a prototype for Intelligent Traffic Management Systems (ITMS).

---

## 📌 Project Overview
Monitoring vehicle speed is critical for road safety and traffic flow optimization. This system processes video feeds to:
1. **Detect** moving objects (vehicles) using Background Subtraction.
2. **Track** individual vehicles across frames using Euclidean Distance.
3. **Calculate** speed by measuring pixel displacement over time.

--- b

## 🎯 Objectives
* Automated detection of vehicles without manual intervention.
* Real-time speed estimation using basic physics ($v = d/t$).
* Visual annotation of speed and bounding boxes on the video output.
* Low-cost implementation using standard OpenCV libraries.

---

## 🛠 Tech Stack
* **Language:** Python 3.x
* **Libraries:** * `OpenCV`: Image processing and vehicle detection.
    * `NumPy`: Mathematical operations and array handling.
* **Tools:** Jupyter Notebook / VS Code.

---

## 📂 Project Structure
```text
speed-detection/
│
├── highway.mp4              # Sample input traffic video
├── main.py                  # Core script for detection & speed calculation
├── tracker.py               # Euclidean Distance Tracking logic
└── README.md                # Project documentation
```
## 🧠 Working Methodology

The project follows a modular pipeline to transform raw video pixels into actionable speed data:



1.  **Background Subtraction**: Uses the `MOG2` algorithm to identify moving pixels by comparing the current frame to a statistical model of the background.
2.  **Contour Detection**: Groups moving pixels into contours and filters them by area to ignore noise (like wind in trees or birds).
3.  **Object Tracking**: Assigns a unique ID to each vehicle using the `EuclideanDistTracker`. It calculates the distance between the center points of objects in consecutive frames to ensure the same car is being tracked.
4.  **Region of Interest (ROI)**: Focuses processing on a specific part of the road to improve performance and accuracy.
5.  **Speed Estimation**: 
    * Tracks the time taken for a vehicle to move between two virtual lines.
    * Converts pixel distance to real-world meters using a calibration constant.
    * Calculates speed using: $$Speed = \frac{Distance}{Time} \times 3.6 \text{ (for km/h)}$$

---

## 📊 Output

When you run the project, the system generates a real-time processed video feed containing:
* **Bounding Boxes**: Visual indicators around every detected vehicle.
* **ID Tracking**: A unique integer assigned to each car that persists across frames.
* **Speedometer**: A text overlay showing the estimated speed in real-time.
* **Mask View**: A binary (black and white) window showing the raw background subtraction results.



---

## 🚧 Limitations & Challenges

* **Perspective Distortion**: Objects further away appear to move slower in pixels than objects closer to the camera. This requires a "Bird's Eye View" wrap for high accuracy.
* **Occlusion**: If one vehicle passes behind another, the tracker may lose the ID or merge two vehicles into one.
* **Weather/Lighting**: Extreme glare, heavy rain, or night-time conditions can interfere with background subtraction.
* **Calibration**: The `pixel_to_meter_ratio` must be manually tuned for every new camera angle or location.

---
