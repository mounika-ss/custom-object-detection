# custom-object-detection
Computer vision task

# Custom Object Detection using YOLOv5 & Roboflow

This project was developed as part of my AI internship at **Mistify AI Technologies**.  
The goal was to build a custom object detection model to detect vehicles such as **cars and trucks** using YOLOv5 and Roboflow with a focus on training accuracy, dataset preparation, and deployment readiness.

---

## Project Objective
To build and train an object detection model using the YOLOv5 algorithm for vehicle detection in images and videos.

## Features
- Used Roboflow for dataset annotation and preprocessing
- YOLOv5 model training and evaluation
- Model performance analysis with confidence thresholds and bounding boxes


---

## Team Collaboration
This was a team task assigned by our mentor.  
I worked with my teammates, and we collaborated on dataset preparation and model training.

---

## Dataset Preparation (Roboflow)

We worked with a dataset that included **train, valid, and test splits** in YOLOv5 format.  
The exported dataset zip had the structure:
```
India cars.v1i.yolov5pytorch/
├── train/
│ ├── images/ (1648 files)
│ └── labels/ (1648 files)
├── valid/
│ ├── images/ (68 files)
│ └── labels/ (68 files)
├── test/
│ ├── images/ (69 files)
│ └── labels/ (69 files)
├── data.yaml
└── README files (dataset info)
```

---

## 🔧 Process & Steps Followed

### **1️⃣ Uploading Dataset in Google Colab**
Since Google Drive mount caused issues, the dataset was uploaded manually:

```python
from google.colab import files
uploaded = files.upload()
```

### 2️⃣ Unzipping the dataset
```python
!unzip "India cars.v1i.yolov5pytorch.zip" -d /content/
```

### 3️⃣ Checking dataset contents
```python
import os
dataset_path = "/content/"
print(os.listdir(dataset_path))
```

---

## 🚀 Model Training (YOLOv5s)
### 4️⃣ Clone YOLOv5 repository
```python
!git clone https://github.com/ultralytics/yolov5
%cd yolov5
!pip install -r requirements.txt
```

### 5️⃣ Train the YOLOv5s model
Used 20 epochs for faster training during internship.
```python
!python train.py --img 640 --batch 16 --epochs 20 --data /content/data.yaml --weights yolov5s.pt --name india_cars_yolov5s
```

After training, all outputs were saved under:

```
runs/train/india_cars_yolov5s/
```

This included:

- best.pt
- training logs
- results charts
- model metrics

---

## 🎥 Vehicle Detection on Video
### 6️⃣ Upload a video
```python
from google.colab import files
uploaded = files.upload()
```

### 7️⃣ Run detection
```python
!python detect.py --weights runs/train/india_cars_yolov5s/weights/best.pt --img 640 --conf 0.25 --source your_video.mp4
```

Output video is saved in:

```
runs/detect/exp/your_video.mp4
```

---

## 🖼️ Detection on Test Images
### 8️⃣ Run detection on test dataset
```python
!python detect.py --weights runs/train/india_cars_yolov5s/weights/best.pt --img 640 --conf 0.25 --source /content/test/images
```

Predicted images are stored in:
```
runs/detect/exp/
```

---
📁 Files Included in This Repository
- Colab notebook PDF (printed output)
- Detected output video (.mp4)
- Reference links
(original video source + tutorial)

References
- YOLOv5 Tutorial:
https://www.youtube.com/watch?v=r0RspiLG260

- Sample Car Video:
https://github.com/jitendrasb24/Car-Detection-OpenCV

- Colab Notebook File:
  [colab link](https://drive.google.com/file/d/1pSJ5DjgxliIW-qPNqSonbm8q26MJsPSO/view?usp=sharing)

### Notes
- The project was completed entirely on Google Colab.
- Dataset annotations were prepared and reviewed using Roboflow.
- YOLOv5s was chosen for training due to its speed and efficiency.

### Conclusion
This project strengthened my skills in:

- Computer Vision
- YOLOv5 model training
- Dataset preparation
- Inference and evaluation
- Google Colab workflow

This repository showcases my learning and implementation during the internship.
