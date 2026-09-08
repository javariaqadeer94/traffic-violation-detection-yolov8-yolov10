# Traffic Object Violation Detection

## Overview

This project presents a comparative evaluation of **YOLOv8 and YOLOv10 object detection models** for traffic-related object detection.

The study investigates the performance of different YOLO model configurations across multiple random seeds to provide a more reliable comparison of detection performance and computational efficiency.

The experiments focus on four models:

* YOLOv8n
* YOLOv8m
* YOLOv10n
* YOLOv10m

Each YOLO model was evaluated using **three random seeds (42, 123, and 456)**. In addition to detection accuracy, the experiments consider computational and deployment-related characteristics such as training time, GPU memory usage, inference speed, and model size.

The experiments were conducted in a **Kaggle GPU environment** using the Ultralytics YOLO framework.
**[View the Kaggle Notebook](*https://www.kaggle.com/code/javeriaqadeer/traffic-object-violation-detection/edit/run/347269201)**

> **Note:** The notebook contains the experimental workflow and saved results from the completed runs. Reproducing the complete training experiments requires the original dataset and access to a suitable GPU.

---

## Research Objective

The primary objective of this project is to compare YOLOv8 and YOLOv10 models of different sizes and examine:

1. Detection performance across multiple random seeds.
2. The effect of model size on detection accuracy.
3. Variation in performance caused by different random seeds.
4. The trade-off between detection accuracy and computational requirements.
5. The practical suitability of lightweight and medium-sized YOLO models for traffic-related object detection.

---

## Models Evaluated

| Model    | Family  | Size   |
| -------- | ------- | ------ |
| YOLOv8n  | YOLOv8  | Nano   |
| YOLOv8m  | YOLOv8  | Medium |
| YOLOv10n | YOLOv10 | Nano   |
| YOLOv10m | YOLOv10 | Medium |

### Experimental Seeds

Each model was evaluated using:

```text
42
123
456
```

This results in a total of:

**4 models × 3 seeds = 12 experimental runs**

---

## Dataset

The project uses a traffic-related object detection dataset containing:

* **23 object classes**
* **5,254 training images**
* **1,470 validation images**

The dataset is not included in this repository.

The experiments were performed using the dataset within the Kaggle environment.

The dataset configuration used during the experiments was:

```text
fixed.yaml
```

Users attempting to reproduce the experiments should obtain the original dataset and recreate the corresponding dataset configuration.

---

## Training Configuration

The YOLO experiments were conducted using a consistent training configuration to ensure a fair comparison between models.

| Parameter             | Setting      |
| --------------------- | ------------ |
| Image Size            | 640 × 640    |
| Epochs                | 100          |
| Batch Size            | 16           |
| Optimizer             | SGD          |
| Initial Learning Rate | 0.01         |
| Momentum              | 0.937        |
| Patience              | 20           |
| Close Mosaic          | 10           |
| Cache                 | True         |
| Workers               | 2            |
| Device                | GPU          |
| Random Seeds          | 42, 123, 456 |

The models were trained using the Ultralytics YOLO framework.

---

## Evaluation Metrics

The models were evaluated using both detection-performance and computational metrics.

### Detection Performance

* **mAP@50**
* **mAP@50:95**
* **Precision**
* **Recall**

### Computational Performance

* **Training Time**
* **GPU Memory Usage**
* **Inference Speed (FPS)**
* **Model Size**

Using multiple seeds allows the study to report not only the average performance but also the variation between runs.

---

## Multi-Seed Evaluation

For each model, the results from the three random seeds are aggregated to calculate:

* Mean performance
* Standard deviation

The primary detection metrics are summarized as:

```text
Mean ± Standard Deviation
```

This provides a more robust representation of model performance than relying on a single training run.

The notebook generates comparative visualizations showing the **Mean ± Standard Deviation** for:

* mAP50
* mAP50-95
* Precision
* Recall

---

## Result Persistence

Because YOLO training is computationally expensive, the notebook uses a JSON-based result persistence mechanism.

The experimental results are stored in:

```text
/kaggle/working/multi_seed_results.json
```

Before starting a training run, the notebook checks whether the corresponding **model + seed combination has already been completed**.

For example:

```text
YOLOv8n + Seed 42
YOLOv8n + Seed 123
YOLOv8n + Seed 456
```

If the result is already recorded with:

```text
status = "done"
```

the corresponding training run is skipped.

This prevents completed experiments from being unnecessarily retrained when a Kaggle session is interrupted or restarted.

---

## Experimental Results

All four models were evaluated using three random seeds (42, 123, and 456), resulting in 12 completed experimental runs.

### Multi-Seed Detection Performance

Results are reported as **mean ± standard deviation** across the three random seeds.

| Model | mAP@50 | mAP@50:95 | Precision | Recall |
|---|---:|---:|---:|---:|
| YOLOv8n | 0.915 ± 0.006 | 0.795 ± 0.006 | 0.892 ± 0.014 | 0.877 ± 0.009 |
| YOLOv8m | **0.924 ± 0.004** | 0.803 ± 0.004 | 0.894 ± 0.018 | **0.892 ± 0.013** |
| YOLOv10n | 0.901 ± 0.005 | 0.786 ± 0.005 | 0.893 ± 0.011 | 0.835 ± 0.012 |
| YOLOv10m | 0.921 ± 0.005 | **0.807 ± 0.002** | **0.902 ± 0.019** | 0.886 ± 0.007 |

### Computational Comparison

| Model | Training Time (min) | GPU Memory (MB) | FPS | Model Size (MB) |
|---|---:|---:|---:|---:|
| YOLOv8n | **102.00 ± 2.32** | **1985.43 ± 39.01** | **69.86 ± 24.28** | 5.95 |
| YOLOv8m | 251.87 ± 131.39 | 5298.62 ± 951.97 | 33.83 ± 2.38 | 49.62 |
| YOLOv10n | 136.56 ± 5.14 | 2682.18 ± 50.17 | 63.13 ± 18.88 | **5.48** |
| YOLOv10m | 391.84 ± 14.26 | 7856.36 ± 39.21 | 36.65 ± 1.82 | 31.95 |

### Key Findings

- **YOLOv10m achieved the highest mAP@50:95** with 0.807 ± 0.002.
- **YOLOv8m achieved the highest mAP@50** with 0.924 ± 0.004.
- **YOLOv10m achieved the highest mean precision** at 0.902 ± 0.019.
- **YOLOv8m achieved the highest mean recall** at 0.892 ± 0.013.
- **YOLOv8n provided the fastest average inference speed** at approximately 69.86 FPS.
- **YOLOv10n was the smallest model** at 5.48 MB.
- The medium-sized models required substantially more GPU memory and training time than the nano models.
- Multi-seed evaluation demonstrates that model rankings can vary depending on the evaluation metric, highlighting the importance of considering both accuracy and computational efficiency.
## Visualizations

The notebook generates comparative plots to analyze model performance.

One of the primary visualizations is:

```text
multi_seed_barplot.png
```

This plot presents:

**Mean ± Standard Deviation**

for the four detection metrics:

* mAP50
* mAP50-95
* Precision
* Recall

across the evaluated YOLO models.

---

## Repository Structure

```text
traffic-object-violation-detection/
│
├── Notebook/
│   └── traffic-object-violiation-detection.ipynb
│
├── outputs/
│   └── multi_seed_barplot.png
│
├── README.md
│
├── requirements.txt
│
└── .gitignore
```

> The exact contents of the `outputs/` directory may vary depending on which experimental artifacts are selected for version control.

---

## Notebook Workflow

The main notebook contains the complete experimental workflow, including:

1. Environment setup
2. GPU verification
3. Dataset preparation
4. Dataset configuration
5. YOLO model configuration
6. Multi-seed training
7. JSON-based result checking
8. Result persistence
9. Model validation
10. Metric extraction
11. Multi-seed aggregation
12. Mean and standard deviation calculation
13. Comparative visualization
14. Model performance analysis

The notebook is designed to avoid unnecessary retraining by checking previously saved experimental results before starting a new run.

---

## Reproducibility

The experiments were originally conducted in a Kaggle GPU environment.

To reproduce the experiments, the following are required:

* Original traffic object detection dataset
* Kaggle or another suitable GPU environment
* Python environment compatible with the notebook
* Ultralytics YOLO
* PyTorch
* Required dependencies listed in `requirements.txt`
* The provided notebook

Because training four models over three seeds requires **12 training runs**, complete reproduction can require substantial GPU time.

The JSON result mechanism can be used to continue experimentation without repeating runs that have already been completed.

---

## Limitations

This project focuses on **comparative object detection performance** rather than developing a complete end-to-end traffic violation recognition system.

The following limitations should therefore be considered:

* The dataset is limited to the available traffic-related object classes.
* Results may vary across datasets and environmental conditions.
* Evaluation is primarily based on the available training and validation data.
* Multi-seed evaluation improves reliability but does not eliminate all sources of experimental variation.
* The experiments were conducted in a Kaggle GPU environment, and computational performance may differ on other hardware.
* The detected traffic-related objects should not automatically be interpreted as confirmed legal traffic violations.

---

## Future Work

Potential future extensions include:

* Evaluation on additional traffic datasets
* Cross-dataset generalization
* Testing under different weather and illumination conditions
* Evaluation on real-world traffic videos
* Cross-domain robustness analysis
* Model compression and quantization
* Knowledge distillation
* Edge-device deployment
* Real-time traffic monitoring
* Integration of object detection with rule-based or vision-based violation recognition
* More extensive statistical analysis across additional random seeds

---

## Author

**Javaria Qadeer**

PhD Researcher | Data Science | Computer Vision | Machine Learning
