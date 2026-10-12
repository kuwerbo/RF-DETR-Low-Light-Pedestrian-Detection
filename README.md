# RF-DETR Nano for Low-Light Pedestrian Detection

## Project Overview

This project fine-tunes the official RF-DETR Nano model for
single-class pedestrian detection under three low-light conditions:
mild, moderate, and severe.

The dataset was derived from a researcher-recorded pedestrian video.
Annotations were manually reviewed and converted into COCO format.

## Objectives

- Prepare and verify a pedestrian-only COCO dataset.
- Train a pretrained RF-DETR Nano detection transformer.
- Evaluate precision, recall, F1-score, IoU, and COCO mAP.
- Compare two learning-rate configurations.
- Analyze predictions and errors under different lighting conditions.

## Model Architecture

The implementation uses the official Roboflow RF-DETR Nano model,
which employs a DINOv2-based vision-transformer backbone.

This project did not independently implement a custom ResNet
backbone or a separate receptive-field enhancement module.

Official framework: https://github.com/roboflow/rf-detr

## Dataset

The dataset originated from a researcher-recorded pedestrian video
and was processed through the earlier low-light pedestrian activities.

Split summary:

| Partition | Source Frames | Images |
|---|---:|---:|
| Training | 140 | 420 |
| Validation | 30 | 90 |
| Test | 30 | 90 |

The source video and complete annotated images are not included
in the public repository.

See `docs/DATASET.md` for preparation details.

## Repository Structure

```text
RF-DETR-Low-Light-Pedestrian-Detection/
├── README.md
├── requirements.txt
├── notebooks/
│   └── RF_DETR_Low_Light_Pedestrian_Detection.ipynb
├── results/
│   └── Evaluation and comparison CSV files
└── docs/
    └── DATASET.md
```

## Installation

Open the notebook in Google Colab and enable GPU acceleration.

Install the required packages:

```bash
pip install -r requirements.txt
```

Mount Google Drive and ensure that the prepared COCO dataset
is accessible under the project directory.

## Training Configuration

The original model training configuration used:

- Model: RF-DETR Nano
- Maximum epochs: 15
- Batch size: 2
- Gradient accumulation: 4
- Optimizer: AdamW
- Learning-rate scheduler: cosine
- Original learning rate: 0.0001
- Experimental learning rate: 0.00005

The library's stopping mechanism used validation detection
performance rather than validation loss.

## Held-Out Test Results

The following results belong to the original trained model.

| Metric | Result |
|---|---:|
| Test Images | 90 |
| True Positives | 334 |
| False Positives | 193 |
| False Negatives | 139 |
| Detection Accuracy (%) | 50.15 |
| Precision (%) | 63.38 |
| Recall (%) | 70.61 |
| F1-score (%) | 66.80 |
| mAP@0.50 (%) | 71.78 |
| mAP@0.50:0.95 (%) | 37.06 |

Detection accuracy is computed as TP/(TP+FP+FN).

## Validation Learning-Rate Comparison

| Model | Precision (%) | Recall (%) | F1 (%) | mAP50 (%) | mAP50:95 (%) |
|---|---:|---:|---:|---:|---:|
| baseline_lr_0001 | 60.24 | 69.07 | 64.35 | 70.11 | 35.01 |
| experiment_lr_00005 | 57.59 | 66.82 | 61.86 | 69.23 | 34.79 |

The model selected using validation mAP@0.50:0.95 was:
**baseline_lr_0001**.

The selected model matches the original checkpoint evaluated on the test set.

## Performance by Lighting Condition

| Lighting | Precision (%) | Recall (%) | mAP50 (%) |
|---|---:|---:|---:|
| Mild | 65.71 | 72.78 | 73.86 |
| Moderate | 61.11 | 72.85 | 73.96 |
| Severe | 63.37 | 66.46 | 68.22 |

## Limitations

- Dataset from a single researcher-recorded video.
- Related low-light image variants.
- Single-class pedestrian detection only.
- One training run per learning-rate configuration.
- No independently implemented receptive-field enhancement module.
- Early stopping did not use validation loss.
- Additional independent low-light datasets are needed.

## Future Work

Further work could investigate additional real-world scenes,
different learning rates, multiple training seeds, data augmentation,
and implementation of a custom receptive-field enhancement module.

## References

1. Robinson et al. (2026). RF-DETR: Real-Time Detection Transformer.
   https://arxiv.org/abs/2511.09554
2. Carion et al. (2020). End-to-End Object Detection with Transformers.
   https://arxiv.org/abs/2005.12872
3. Lin et al. (2014). Microsoft COCO: Common Objects in Context.
   https://arxiv.org/abs/1405.0312
4. Oquab et al. (2024). DINOv2.
   https://arxiv.org/abs/2304.07193
5. Roboflow RF-DETR official repository.
   https://github.com/roboflow/rf-detr
