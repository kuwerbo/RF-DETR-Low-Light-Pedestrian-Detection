# Dataset Preparation

## Source

The source data came from a researcher-recorded pedestrian video.
Frames were extracted, processed under mild, moderate, and severe
low-light conditions, and manually reviewed during previous activities.

## Annotation Format

The verified YOLO annotations were converted into COCO format.

The dataset contains one object category: person.

## Expected Directory Structure

```text
dataset/rfdetr_coco/
    train/
        _annotations.coco.json
        image_files...
    valid/
        _annotations.coco.json
        image_files...
    test/
        _annotations.coco.json
        image_files...
```

## Splitting

The original source frames were divided into training, validation,
and test sets before grouping the related lighting variants.

## Availability

The original video, full image dataset, and trained weights are
not included in this public GitHub repository.

To reproduce the experiments, authorized access to the original
dataset is required, and Google Drive paths may need to be updated.

## Assignment Requirement Difference

The assignment specifies a dataset from Kaggle or Roboflow.
This project's original data came from a researcher-recorded video.
Instructor approval is therefore required for that substitution.
