# SLICE-3D 2024 Challenge Dataset

## Overview
The SLICE-3D dataset is designed for skin lesion classification using images extracted from 3D Total Body Photography (TBP). The goal is to differentiate between benign and malignant cases using diagnostically labeled images with associated metadata. The dataset includes:

- **Images**: JPEG lesion images.
- **Metadata**: A CSV file with clinical and image-based features.
- **Binary Classification Target**: 0 for benign, 1 for malignant.

## Dataset Description
### Files Included:
- `train-image/` - Folder containing JPEG training images.
- `train-image.hdf5` - HDF5 file with training image data, indexed by `isic_id`.
- `train-metadata.csv` - Metadata for training images.
- `test-image.hdf5` - HDF5 file with test image data.
- `test-metadata.csv` - Metadata for test images.
- `sample_submission.csv` - Example submission format.

### Metadata Fields
The metadata includes:
- **Patient Details**: `age_approx`, `sex`, `patient_id`.
- **Lesion Information**: `lesion_id`, `anatom_site_general`, `clin_size_long_diam_mm`, `tbp_lv_areaMM2`, etc.
- **Image-Based Features**: `tbp_lv_H`, `tbp_lv_L`, `tbp_lv_norm_border`, `tbp_lv_radial_color_std_max`, etc.
- **Classification Labels** (only in `train-metadata.csv`): `target` (0: benign, 1: malignant).

## Data Imbalance and Preprocessing
The dataset is **highly imbalanced**, with 99% benign and 1% malignant cases. To handle this:
- **Undersampling and Oversampling** techniques are applied to balance the dataset.
- **Augmentations** such as flipping, rotation, and color shifts are used to enhance model robustness.

## Model and Dataloader
- **Model Architecture**: `EfficientNetV2Backbone` is used for feature extraction from lesion images.
- **Dataloader Setup**:
  - Incorporates both **tabular metadata** and **image data**.
  - Images are normalized and resized before being fed into the model.
  - Tabular features are preprocessed and concatenated with image embeddings for classification.

