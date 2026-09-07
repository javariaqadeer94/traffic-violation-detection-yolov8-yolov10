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

Notebook

The main notebook contains the complete experimental workflow, including:

Environment and GPU setup
Dataset preparation
Model configuration
YOLOv8 experiments
YOLOv10 experiments
Multi-seed evaluation
Additional detector comparisons
Performance evaluation
Results analysis
Model comparison

The notebook is provided with its saved outputs from the completed Kaggle
experiments.

Reproducibility

The experiments were originally executed in a Kaggle GPU environment.

Because object detection training is computationally expensive, this
repository does not include the complete dataset or trained model
weights.

To reproduce the experiments, the user needs:

The original dataset
A suitable GPU environment
The dependencies listed in requirements.txt
The provided notebook
Limitations

This project focuses on comparative object detection performance.
Therefore, the presence of traffic-related object classes should not be
interpreted as a complete end-to-end traffic violation recognition
system.

Future Work

Potential future improvements include:

Evaluation on additional traffic datasets
Cross-dataset generalization
More extensive real-world testing
Model compression and optimization
Deployment on edge devices
Analysis under different environmental conditions
Author

Javaria Qadeer

PhD Researcher | Data Science | Computer Vision | Machine Learning

├── requirements.txt
└── .gitignore
