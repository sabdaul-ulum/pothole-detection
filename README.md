# Pothole and Road Damage Detection

This repository contains the codebase for a comprehensive Pothole and Road Damage Detection project. The primary objective is to detect and classify various types of road damage effectively using state-of-the-art computer vision models, including **RT-DETR** (Real-Time DEtection TRansformer) and various iterations of the **YOLO** architecture (YOLOv8, YOLO11, and YOLO26).

This research-oriented project aims to compare Transformer-based architectures against traditional and modern CNN-based architectures for road damage scenarios, focusing on achieving a balance between high accuracy and real-time inference speed.

## 🚀 Key Features

- **Data Preprocessing**: Scripts to clean and convert hybrid bounding box and polygon annotations (such as the N-RDD2024 format) into the standard YOLO format.
- **Model Training**: comprehensive Jupyter notebooks configured for training multiple object detection models including:
  - RT-DETR (Large)
  - YOLOv8 (Large)
  - YOLO11 (Large)
  - YOLO26 (Large)
- **Performance Evaluation**: Built-in validation metrics and plots that are automatically generated for each training run, enabling robust comparative analysis.

## 📂 Project Structure

```text
pothole-detection/
│
├── configs/
│   └── dataset.yaml         # Configuration file defining dataset paths and classes
├── dataset/
│   ├── train/               # Training images and YOLO format labels
│   ├── val/                 # Validation images and YOLO format labels
│   └── test/                # Testing images and labels
├── runs/                    # Output directory for Ultralytics training runs (weights, plots, etc.)
├── src/                     # Source scripts and Jupyter notebooks
│   ├── 00_fix_dataset.ipynb # Preprocessing notebook to standardize labels
│   ├── 01_train_rtdetr.ipynb# Training notebook for the RT-DETR model
│   ├── 02_train_yolov8.ipynb# Training notebook for the YOLOv8 model
│   ├── 03_train_yolo11.ipynb# Training notebook for the YOLO11 model
│   ├── 04_train_yolo26.ipynb# Training notebook for the YOLO26 model
├── trained_weights/         # Best model checkpoints saved locally
└── README.md                # Project documentation
```

## 📊 Dataset Information

The project utilizes a custom-built dataset constructed by merging and refining two distinct sources:
1. **N-RDD2024 (Road damage and defects)**: The dataset from all participating countries in the N-RDD2024 challenge was unified.
2. **Multi-Weather Pothole Detection (MWPD)**: Added additional diversity to lighting and weather conditions.

As part of this project, the dataset labels were extensively cleaned. Irregular formats (like hybrid polygon coordinates) were normalized into standard YOLO bounding boxes. Crucially, the dataset has been filtered and remapped to support a **single-class configuration**.

- **Class**: `pothole` (representing all identified potholes from both datasets; other damage types such as cracks were excluded).

**Dataset Download Link:**
As the dataset is too large to host directly on GitHub, you can download the compiled dataset from:
- [Dataset Link](https://binusianorg-my.sharepoint.com/personal/asep_firmansyah_binus_ac_id/Documents/Binus/Skripsi/Dataset/dataset.zip?csf=1&web=1&e=h3yiaI)

**Dataset Breakdown**:
- **Train**: 4,008 images
- **Validation**: 410 images
- **Test**: 239 images
- **Total**: 4,657 images 

## ⚙️ Installation & Prerequisites

1. Ensure you have **Python 3.10+** installed.
2. Set up a virtual environment using `uv` (recommended):
   ```bash
   uv venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```
3. Install the required libraries (including PyTorch and Ultralytics):
   ```bash
   uv pip install ultralytics opencv-python tqdm jupyter
   ```
   *(Ensure you install the PyTorch version that corresponds to your CUDA version if you are utilizing GPU acceleration).*

## 📖 Usage

### 1. Formatting Dataset Annotations
If your dataset annotations contain polygon coordinates or incorrect formats, use the data preparation script to normalize them to the standard YOLO bounding box format:
- Launch `src/00_fix_dataset.ipynb` in Jupyter Notebook or Jupyter Lab.
- Execute the cells to process the `train` and `val` directories.

### 2. Training Models
To train the selected models on the prepared dataset:
- Open the corresponding training notebook (e.g., `src/01_train_rtdetr.ipynb` or `src/02_train_yolov8.ipynb`).
- Run the hardware acceleration cell to verify that CUDA is accessible.
- Adjust hyperparameters if necessary (e.g., batch size, image dimensions, number of epochs).
- Run the entire notebook. Results (including weights, loss plots, and PR curves) will be stored in the `runs/` directory (e.g., `runs/detect/train/`).
