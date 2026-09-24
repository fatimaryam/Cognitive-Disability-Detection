# Cognitive-Disability-Detection
Official implementation and experimental code for multi-drawing Transformer-based cognitive disability screening.

**An Interpretable Multi-Task Deep Learning Framework for Automated Cognitive Disability Detection Using Cognitive Drawing Assessments**

## Overview

This repository contains the implementation, experimental notebooks, and results for an automated cognitive disability screening framework based on multiple hand-drawn cognitive assessments.

The framework jointly analyzes three cognitive drawing tasks:

* **Clock Drawing**
* **Copy Drawing**
* **Trail Drawing**

The task is formulated as binary classification using labels derived from the Montreal Cognitive Assessment (MoCA) score:

* **MoCA < 25 → MCI**
* **MoCA ≥ 25 → Normal**

The proposed framework uses an **EfficientNet-B3 image encoder**, a **Transformer-based cross-drawing representation module**, and **feature-preserving attention fusion** to integrate information from the three cognitive drawing tasks.

## Dataset

The dataset contains **918 patients**:

| Class     | Patients |
| --------- | -------: |
| Normal    |      651 |
| MCI       |      267 |
| **Total** |  **918** |

The data are divided at the **patient level** to prevent data leakage between training, validation, and test sets.

| Split      | Patients |
| ---------- | -------: |
| Training   |      642 |
| Validation |      138 |
| Test       |      138 |
| **Total**  |  **918** |

The experiments use:

```text
SEED = 42
```

The dataset itself is **not included in this repositor**.

### Dataset Access

The dataset should be obtained from its original source and used according to the applicable dataset terms and conditions.

**Dataset:** [https://github.com/cccnlab/MCI-multiple-drawings]

## Repository Structure

```text
multi-drawing-transformer-fusion/
│
├── README.md
│
├── notebooks/
│   ├── Baseline_Models.ipynb
│   ├── finetune_(Proposed_Model).ipynb
│   └── Report_Generation.ipyn
│
└── results/
    ├── plots/
    └── gradcam-results/
    └── reports/
```

## Notebooks

### 01 — Baselines Models

This notebook contains:

* Dataset loading
* Patient-level data splitting
* Image preprocessing
* Data augmentation
* Class distribution analysis
* Baseline model training
* Baseline evaluation

The baseline architectures include:

* DenseNet-121
* EfficientNet-B3
* ViT-B/16
* ConvNeXt-Tiny

### 02 — Finetune (Proposed Model)

This notebook contains the implementation and evaluation of the proposed multi-drawing framework.

The proposed architecture includes:

1. Individual feature extraction from the three cognitive drawings
2. Cross-drawing representation using a Transformer
3. Feature-preserving attention fusion
4. Binary classification
5. Model evaluation
6. Performance analysis

### 03 — Grad-CAM and LLM Reports

This notebook contains the explainability and automated reporting components.

It includes:

* Grad-CAM visualization
* Task-specific visual explanations
* Model prediction analysis
* Automated diagnostic report generation
* Explainability examples

## Preprocessing

The experiments use task-specific image preprocessing and augmentation.

The main training augmentations include:

* Rotation within a small range
* Translation
* Scaling
* Brightness adjustment
* Contrast adjustment

Horizontal flipping and large rotations are avoided because the spatial orientation and structure of the cognitive drawings can contain diagnostically relevant information.

## Training Configuration

The main experimental settings include:

```text
Random seed:        42
Image size:         300 × 300
Batch size:         16
Learning rate:      1e-4
Weight decay:       1e-4
Maximum epochs:     50
Early stopping:     10 epochs
Mixed precision:    Enabled
```

The proposed framework uses an EfficientNet-B3 feature representation together with a Transformer-based cross-drawing module and attention-based feature fusion.

## Results

Evaluation is performed on the held-out test set containing **138 patients**.

The main proposed-model test results are:

| Metric      |  Value |
| ----------- | -----: |
| Accuracy    | 77.54% |
| AUC         |  0.742 |
| Precision   | 76.47% |
| Recall      | 32.50% |
| Specificity | 95.92% |
| F1-score    |  0.456 |

The reported confusion matrix at the selected threshold is:

|                   | Predicted Normal | Predicted MCI |
| ----------------- | ---------------: | ------------: |
| **Actual Normal** |               94 |             4 |
| **Actual MCI**    |               27 |            13 |

Additional performance plots and tables are available in:

```text
results/
├── plots/
├── reports/
└── gradcam-results/
```

## Explainability

Grad-CAM is used to visualize image regions that contribute to the model's predictions for the individual cognitive drawing tasks.

The generated visual explanations are intended to provide insight into which regions of the drawings influence the model's output.

Example visualizations are provided in:

```text
results/plots/
```

## Automated Diagnostic Reports

The repository also contains code for generating automated diagnostic reports using model predictions and visual explanation information.

The reporting component is designed to convert model outputs and explainability information into a structured, human-readable report.

The report-generation implementation is available in:

```text
notebooks/03_gradcam_and_llm_reports.ipynb
```

## Reproducing the Experiments

### 1. Clone the repository

```bash
git clone https://github.com/fatimaryam/Cognitive-Disability-Detection.git
cd Cognitive-Disability-Detection
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Prepare the dataset

Place the dataset on your Google Drive or local machine.

The original experimental notebooks use:

```text
/content/drive/MyDrive/MCI_dataset
```

If your dataset is stored at another location, update the dataset path in the notebooks.

### 4. Run the notebooks

Run the notebooks in the following order:

```text
01 → 02 → 03
```

This order follows the experimental workflow from preprocessing and baseline models to the proposed framework and explainability/report generation.

## Hardware

The experiments were developed and tested using **Google Colab with GPU acceleration**.

GPU availability and training time may vary depending on the hardware environment.

## Reproducibility

To improve reproducibility:

* Patient-level splitting is used.
* Random seed is fixed to **42**.
* Training configurations are documented in the notebooks.
* Evaluation is performed on a held-out test set.
* The dataset is not redistributed through this repository.

## Important Note About the Dataset

This repository contains the **code and experimental results**, but does not redistribute the patient dataset or patient images.

Users must obtain the dataset through its original source and comply with all applicable terms, permissions, privacy requirements, and usage restrictions.

## Citation

If you use this repository or build upon this work, please cite the associated research paper:

```bibtex
@article{sirshar2026cognitivedisability,
  title   = {An Interpretable Multi-Task Deep Learning Framework for Automated Cognitive Disability Detection Using Cognitive Drawing Assessments},
  author  = {[ADD AUTHORS]},
  journal = {[ADD JOURNAL]},
  year    = {2026}
}
```

## License

The source code in this repository is released under the **MIT License**.

See the `LICENSE` file for the complete license terms.

The dataset is **not covered by this repository's MIT License** and remains subject to its original terms of use.

## Contact

For questions regarding the implementation or research work, please contact the corresponding author through the contact information provided in the associated publication.
