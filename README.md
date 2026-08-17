# 🎯 Face Recognition Attendance System

A Python-based **automated attendance management system** that uses computer vision and machine learning to identify students through facial recognition and record their attendance with timestamps.

The system captures facial samples through a webcam, trains a **K-Nearest Neighbors (KNN)** classifier, recognizes registered students in real time, and stores daily attendance records in CSV files.

---

## 📌 Project Overview

Traditional attendance systems require teachers to manually call names or maintain physical registers, which can be time-consuming and prone to human error.

This project automates the process using **face detection and face recognition**.

A student can register their face once, after which the system can identify them through a webcam and record their attendance along with the exact time.

### Core Workflow

```text
Student Registration
        ↓
Capture Face Samples
        ↓
Store Face Data
        ↓
Train KNN Classifier
        ↓
Real-Time Face Detection
        ↓
Face Recognition
        ↓
Student Identification
        ↓
Attendance Recorded
        ↓
Daily CSV Report
```

---

## ✨ Features

### 👤 Face Registration

The system allows a new student to register by entering their name and capturing facial samples through the webcam.

During registration:

* Webcam captures the student's face
* Haar Cascade detects the face
* Face images are cropped and resized
* 100 facial samples are collected
* Facial data is stored locally
* Student names are associated with the captured samples

The registration process is implemented in `add_faces.py`.

---

### 🤖 Face Recognition

The system uses:

* OpenCV for webcam input and face detection
* Haar Cascade Classifier for detecting faces
* KNN for identifying registered students

During recognition, the detected face is resized to the same dimensions used during training and passed to the KNN classifier to predict the student's identity.

---

### 🕐 Automated Attendance

Once a student is recognized, the system generates an attendance record containing:

```text
NAME
TIME
```

Attendance is stored in a daily CSV file using the format:

```text
Attendance/Attendance_DD-MM-YYYY.csv
```

This creates a separate attendance file for each day.

---

### 🔊 Voice Confirmation

The system uses Windows Speech API through `win32com.client` to provide voice feedback when attendance is taken.

For example:

```text
"Attendance Taken.."
```

This gives the user an audio confirmation after pressing the attendance key.

---

### 📊 Attendance Dashboard

A Streamlit-based application is included for displaying the attendance data.

The application automatically loads the CSV corresponding to the current date and displays the records using a Streamlit dataframe.

---

## 🛠️ Tech Stack

| Technology              | Purpose                               |
| ----------------------- | ------------------------------------- |
| **Python**              | Core programming language             |
| **OpenCV**              | Webcam processing and computer vision |
| **Haar Cascade**        | Face detection                        |
| **Scikit-learn**        | KNN machine-learning classifier       |
| **NumPy**               | Numerical and matrix operations       |
| **Pandas**              | Attendance data handling              |
| **Pickle**              | Local face/label data storage         |
| **CSV**                 | Attendance record storage             |
| **Streamlit**           | Attendance dashboard                  |
| **PyWin32**             | Voice feedback through Windows SAPI   |
| **HTML/CSS/JavaScript** | Basic attendance portal interface     |

The repository includes Python scripts for registration, recognition, testing, and the Streamlit viewer, along with a basic web portal.

---

## 📂 Project Structure

```text
Attendence-System/
│
├── Attendance/
│   └── Attendance_DD-MM-YYYY.csv
│
├── data/
│   ├── haarcascade_frontalface_default.xml
│   ├── names.pkl
│   └── faces_data.pkl
│
├── Attendance/
│
├── Login.html
├── main.html
├── script.js
├── stylee.css
│
├── add_faces.py
├── app.py
├── test.py
│
├── xyz.jpg
├── xyzz.png
│
└── README.md
```

The current repository contains the `Attendance` and `data` directories along with the Python scripts and web-interface files shown above.

---

## ⚙️ How It Works

### Step 1 — Register a Student

Run:

```bash
python add_faces.py
```

Enter the student's name when prompted:

```text
Enter Your Name:
```

The webcam opens and captures up to **100 face samples** for the student.

The captured data is stored in:

```text
data/faces_data.pkl
```

and the corresponding names are stored in:

```text
data/names.pkl
```

---

### Step 2 — Start Face Recognition

Run:

```bash
python test.py
```

The program:

1. Opens the webcam
2. Detects faces
3. Loads registered face data
4. Trains a KNN classifier
5. Predicts the detected student's name
6. Displays the recognized name on the video feed
7. Records attendance when the attendance key is pressed

The current implementation uses:

```python
KNeighborsClassifier(n_neighbors=5)
```

for classification.

---

### Step 3 — Mark Attendance

When the student's face is recognized, press:

```text
O
```

The system provides voice confirmation and writes the student's name and timestamp into the day's attendance CSV file.

Press:

```text
Q
```

to exit the recognition window.

---

### Step 4 — View Attendance

Run the Streamlit application:

```bash
streamlit run app.py
```

The dashboard loads the current day's attendance CSV and displays the records in a table.

---

## 🧠 Machine Learning Approach

The project uses a **K-Nearest Neighbors (KNN)** classifier.

### Training

Registered face images are:

```text
Face Image
    ↓
Face Detection
    ↓
Crop Face
    ↓
Resize → 50 × 50
    ↓
Flatten Pixel Values
    ↓
KNN Training Data
```

The training data and labels are loaded from:

```text
faces_data.pkl
names.pkl
```

The KNN model is configured with:

```python
KNeighborsClassifier(n_neighbors=5)
```

and trained using the stored face matrix and corresponding labels.

---

## 📸 Face Detection

The project uses OpenCV's Haar Cascade classifier:

```text
data/haarcascade_frontalface_default.xml
```

The webcam frame is converted to grayscale before face detection:

```python
gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
```

The detected face is then cropped and resized before being passed to the recognition pipeline.

---

## 📊 Attendance Data Format

Attendance is stored as CSV files:

```text
Attendance/
    ├── Attendance_15-08-2026.csv
    ├── Attendance_16-08-2026.csv
    └── Attendance_17-08-2026.csv
```

Each file contains:

```csv
NAME,TIME
Lakshya,10:30-15
Rahul,10:32-08
Aman,10:34-21
```

This makes the records easy to open and analyze using Excel, Pandas, or other data-analysis tools.

---

## 🖥️ Basic Web Portal

The repository also contains a basic attendance portal built with HTML, CSS, and JavaScript.

The portal provides two primary actions:

```text
┌──────────────────────────────┐
│      Attendance Portal       │
│                              │
│   [ Mark Attendance ]        │
│                              │
│   [ New Registration ]       │
└──────────────────────────────┘
```

The interface is implemented through `main.html`, `script.js`, and `stylee.css`.

---

## 🚀 Installation

### Prerequisites

Make sure you have:

* Python 3.x
* Webcam
* Windows OS recommended for voice feedback
* Git

---

### Clone the Repository

```bash
git clone https://github.com/Lakshya172/Attendence-System.git
```

Navigate to the project:

```bash
cd Attendence-System
```

---

### Install Dependencies

```bash
pip install opencv-python
pip install numpy
pip install pandas
pip install scikit-learn
pip install streamlit
pip install streamlit-autorefresh
pip install pywin32
```

---

## ▶️ Running the Project

### Register a Student

```bash
python add_faces.py
```

### Start Recognition

```bash
python test.py
```

### Start Attendance Dashboard

```bash
streamlit run app.py
```

---

## ⚠️ Important Notes

### Camera Required

The system uses:

```python
cv2.VideoCapture(0)
```

so a working webcam is required.

### Windows Voice Support

The current recognition script uses:

```python
from win32com.client import Dispatch
```

for Windows SAPI voice output, so this feature is intended for Windows environments.

### Local Data Storage

Face data is stored locally using Pickle files:

```text
data/names.pkl
data/faces_data.pkl
```

Attendance records are stored as CSV files rather than in a cloud database.

---

## 🔮 Future Improvements

The project can be extended into a production-ready attendance platform by adding:

* [ ] MongoDB/PostgreSQL database
* [ ] Secure user authentication
* [ ] Teacher/admin dashboard
* [ ] Student dashboard
* [ ] Attendance percentage calculation
* [ ] Monthly and semester reports
* [ ] Duplicate attendance prevention
* [ ] Email notifications
* [ ] Cloud storage
* [ ] REST API
* [ ] Mobile application
* [ ] Better face-recognition models
* [ ] Liveness detection
* [ ] Role-based access control
* [ ] Export reports to Excel/PDF
* [ ] Deploy the dashboard online

---

## 🎓 Learning Outcomes

Through this project, I gained practical experience with:

* Computer Vision
* Face Detection
* Face Recognition
* Machine Learning Classification
* OpenCV
* KNN Algorithm
* Webcam Processing
* Python File Handling
* CSV Data Management
* Pickle Serialization
* Streamlit
* Basic Web Development
* Real-time Application Development

---

## 👨‍💻 Author

**Lakshya Agarwal**

B.Tech Computer Science & Engineering
Lovely Professional University

GitHub:
https://github.com/Lakshya172

---

## ⭐ Project

If you find this project useful, consider giving the repository a ⭐.

**Repository:**
https://github.com/Lakshya172/Attendence-System

---

## 📄 License

This project was created for **educational and learning purposes**.
