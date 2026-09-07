# Traffic Object Violation Detection

## Overview

This project presents a comparative evaluation of deep learning-based
object detection models for traffic-related object detection.

The study evaluates YOLOv8 and YOLOv10 models using multiple model
configurations and random seeds, with additional comparisons against
RT-DETR and Faster R-CNN.

The experiments were conducted using GPU-based training on Kaggle.

> **Note:** The notebook contains completed experimental runs and saved
> outputs. Re-running the complete training pipeline requires the original
> dataset and GPU resources.

---

## Models Evaluated

- YOLOv8n
- YOLOv8m
- YOLOv10n
- YOLOv10m
- RT-DETR-L
- Faster R-CNN

---

## Evaluation

The models were evaluated using multiple performance metrics, including:

- mAP@50
- mAP@50:95
- Precision
- Recall
- Inference speed / FPS
- GPU memory usage
- Model size
- Training time

Multiple random seeds were used for the YOLO experiments to provide a
more robust comparison of model performance.

---

## Dataset

The dataset is not included in this repository.

The original dataset was used through the Kaggle environment for model
training and evaluation.

Please refer to the original dataset source before attempting to
reproduce the experiments.

---

## Repository Structure

```text
traffic-object-violation-detection/
│
├── Notebook/
│   └── traffic-object-violiation-detection.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
