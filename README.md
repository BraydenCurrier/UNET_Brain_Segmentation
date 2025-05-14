# Brain Tumor Segmentation with 3D U-Net

This repository contains code for segmenting brain tumors from 3D MRI scans using a customized 3D U-Net architecture. The model is trained on the BraTS 2023 dataset and employs a hybrid loss function—combining Dice Loss and Categorical Crossentropy—to improve segmentation accuracy across complex tumor subregions.

## Project Overview

Glioblastoma multiforme (GBM) is a highly aggressive brain tumor that requires accurate segmentation for effective diagnosis and treatment planning. This project focuses on the automatic segmentation of tumor subregions, including edema, enhancing tumor, and necrotic tissue, using deep learning techniques applied to volumetric MRI data.

## Dataset

- **Source:** [BraTS 2023 Glioma Challenge](https://www.kaggle.com/datasets/luumsk/asnr-miccai-brats-2023-gli-challenge-training-data)
- **Modalities used:** T1, T1CE, T2, FLAIR
- **Mask labels:**
  - 0: Background
  - 1: Necrotic/Non-enhancing tumor
  - 2: Edema
  - 4: Enhancing tumor

Note: Only 989 of the 1,253 available samples were used due to missing or corrupted files.

## Model Architecture

The implemented model follows a standard 3D U-Net architecture with the following components:
- Encoder-decoder structure with skip connections
- Three downsampling and upsampling stages
- Batch normalization and ReLU activation
- Softmax output layer for five-class voxel-wise classification

## Training Details

- **Input dimensions:** 240 × 240 × 160 × 4
- **Loss function:** Dice Loss + Categorical Crossentropy
- **Optimizer:** Adam
- **Precision:** Mixed precision (float16)
- **Epochs:** Trained to epoch 3; however, due to a checkpoint corruption issue, evaluation was conducted using the epoch 2 model.

## Results

The model achieved the following performance metrics on the validation set:

| Metric         | Value |
|----------------|-------|
| Dice Score     | 0.87  |
| Intersection over Union (IoU) | 0.79  |
| F1 Score       | 0.88  |

Despite the inability to evaluate the final epoch, the model demonstrated strong performance in segmenting key tumor regions.

## Visual Outputs

The notebook includes visualization examples of:
- Input modality slices
- Ground truth segmentation masks
- Model predictions
- Color-coded overlay comparisons
