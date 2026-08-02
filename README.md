# 🚗 Parking Spot Occupancy Detector

A real-time computer vision system that monitors parking spaces from a video stream and automatically determines whether each parking spot is **occupied** or **available** using a machine learning classifier.

The system detects predefined parking spaces, classifies each one using a trained Support Vector Machine (SVM), and overlays the results directly on the video with a live counter showing the number of available parking spots.

---

## 📌 Features

- Real-time parking space occupancy detection
- Automatic classification of each parking spot as:
  - 🟢 Empty
  - 🔴 Occupied
- Live visualization using OpenCV
- Displays available parking spaces in real time
- Optimized processing by updating only spots that have changed
- Lightweight implementation suitable for smart parking applications

---

## 🖥️ Demo

The system performs the following steps:

1. Reads a parking lot video.
2. Detects predefined parking spaces from a binary mask.
3. Crops every parking spot.
4. Classifies each spot using a trained SVM model.
5. Draws:
   - Green rectangles for empty spots
   - Red rectangles for occupied spots
6. Displays the total number of available parking spaces.

---

## ⚙️ How It Works

### 1. Parking Spot Localization

Parking spaces are predefined using a binary mask image (`mask_1920_1080.png`).

Each white region in the mask represents a parking space.

OpenCV's `connectedComponentsWithStats()` extracts all connected regions and generates a bounding box for every parking spot.

---

### 2. Parking Space Classification

Each detected parking space is:

- Cropped from the current frame
- Resized to **15 × 15 pixels**
- Flattened into a feature vector
- Passed to a trained Support Vector Machine (SVM)

The classifier predicts:

- **Empty**
- **Occupied**

---

### 3. Performance Optimization

Running the classifier on every parking space in every frame is computationally expensive.

To improve efficiency:

- The system performs a full update every **30 frames**
- The average pixel intensity difference is computed between the current frame and the previous processed frame
- Only parking spaces whose appearance changed significantly are reclassified

This greatly reduces unnecessary predictions while maintaining accurate real-time performance.

---

## 🧠 Machine Learning Model

| Property | Value |
|----------|-------|
| Model | Support Vector Machine (SVM) |
| Library | scikit-learn |
| Kernel | RBF |
| Input Size | 15 × 15 × 3 |
| Feature Vector | 675 values |
| Output Classes | Empty / Occupied |

The trained model is stored as:

```
model.p
```

and loaded using Python Pickle.

---

## 🛠️ Tech Stack

- Python
- OpenCV
- NumPy
- scikit-learn
- scikit-image
- Pickle

---

## 📂 Project Structure

```
parking-spot-occupancy-detector/
│
├── main.py
├── util.py
├── model.p
├── mask_1920_1080.png
├── requirements.txt
├── Video Project2.mp4
└── README.md
```

---

## 🚀 Installation

Clone the repository

```bash
git clone https://github.com/yourusername/parking-spot-occupancy-detector.git
```

Create a virtual environment

```bash
python -m venv venv
```

Activate it

**Windows**

```bash
venv\Scripts\activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Run

```bash
python main.py
```

Press **Q** to exit.

---

## 📈 Future Improvements

- Replace the SVM with a deep learning model such as YOLOv8 or MobileNet.
- Support live IP cameras instead of prerecorded videos.
- Store parking statistics in a database.
- Build a web dashboard for monitoring parking availability.
- Detect incorrectly parked vehicles.
- Estimate parking duration for each vehicle.

---

## 📚 Applications

- Smart parking systems
- Shopping malls
- Airports
- Universities
- Office buildings
- Smart city infrastructure

---

## 👨‍💻 Author

**Mohamed Essam**

Computer Science & Artificial Intelligence Student

Interested in Computer Vision, Machine Learning, and Data Science.
