# Brain Tumor Classification and Survival Prediction
Welcome to the Brain Tumor Classification and Survival Prediction project! This repository contains code and resources for classifying brain tumors and predicting survival rates using machine learning techniques.
## Table of Contents
* Introduction
* Dataset
* Usage
* Models
* Contribution
* Results
* Licenses
## Introduction
Brain tumor classification and survival prediction are crucial tasks in medical diagnostics and treatment planning. This project aims to develop machine learning models capable of accurately classifying brain tumors from medical images and predicting patient survival rates based on various clinical factors.

This project engages in the intricate task of segmenting preoperative MRI images while simultaneously incorporating survival prediction. Our primary aim is to accurately classify each pixel within the image, discerning its association with specific tumor regions. The subregions under scrutiny include the enhancing tumor (ET), the tumor core (TC), and the entire tumor (WT).

Our segmentation approach involves assigning distinct numerical values to delineate various regions:

NCR & NET (Necrosis and Non-Enhancing Tumor): Indicated by the value 1. ED (Edema): Represented by the value 2. ET (Enhancing Tumor): Highlighted with the value 4. Pixels outside these regions: Designated with the value 0 in the segmentation labels. This project presents a comprehensive solution, covering intricate data manipulation and sophisticated 3D visualization techniques. By leveraging the U-Net architecture for segmentation, we meticulously evaluate performance using metrics such as the Dice coefficient.

Moreover, our methodology integrates survival prediction techniques. Through advanced machine learning methods, we prognosticate patient survival rates based on diverse clinical factors. This holistic approach has the potential to significantly advance neurological diagnostics, offering precise tumor segmentation alongside valuable insights into patient prognosis.
## Dataset
BraTS has always been focusing on the evaluation of state-of-the-art methods for the segmentation of brain tumors in multimodal magnetic resonance imaging (MRI) scans. BraTS 2020 utilizes multi-institutional pre-operative MRI scans and primarily focuses on the segmentation (Task 1) of intrinsically heterogeneous (in appearance, shape, and histology) brain tumors, namely gliomas. Furthemore, to pinpoint the clinical relevance of this segmentation task, BraTS’20 also focuses on the prediction of patient overall survival (Task 2), and the distinction between pseudoprogression and true tumor recurrence (Task 3), via integrative analyses of radiomic features and machine learning algorithms. Finally, BraTS'20 intends to evaluate the algorithmic uncertainty in tumor segmentation (Task 4).

Tasks' Description and Evaluation Framework In this year's challenge, 4 reference standards are used for the 4 tasks of the challenge:

* Manual segmentation labels of tumor sub-regions,
* Clinical data of overall survival,
* Clinical evaluation of progression status,
* Uncertainty estimation for the predicted tumor sub-regions.
  
**Imaging Data Description**

All BraTS multimodal scans are available as NIfTI files (.nii.gz) and describe a) native (T1) and b) post-contrast T1-weighted (T1Gd), c) T2-weighted (T2), and d) T2 Fluid Attenuated Inversion Recovery (T2-FLAIR) volumes, and were acquired with different clinical protocols and various scanners from multiple (n=19) institutions, mentioned as data contributors here.

All the imaging datasets have been segmented manually, by one to four raters, following the same annotation protocol, and their annotations were approved by experienced neuro-radiologists. Annotations comprise the GD-enhancing tumor (ET — label 4), the peritumoral edema (ED — label 2), and the necrotic and non-enhancing tumor core (NCR/NET — label 1), as described both in the BraTS 2012-2013 TMI paper and in the latest BraTS summarizing paper. The provided data are distributed after their pre-processing, i.e., co-registered to the same anatomical template, interpolated to the same resolution (1 mm^3) and skull-stripped.

**To download Dataset**
   ```bash
   !kaggle datasets download -d awsaf49/brats20-dataset-training-validation
   ```
---

## Usage

To use the code in this repository, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/goutham-senapathi/5082-Project.git

2. To install the libraries
   ```bash
	pip install -r requirements.txt

## Models
To construct and compile the UNet model in Keras, the following steps are taken:

**1. Building the UNet Model**
The UNet model is built using the build_unet function, which takes parameters such as the input layer, initializer, and dropout rate. This function defines the architecture of the UNet model, including encoder and decoder blocks, followed by an output layer.

```bash
model = build_unet(input_layer, 'he_normal', 0.2)
```

**2. Compiling the Model**
After building the UNet model, it is compiled using the compile() method. During compilation, the loss function, optimizer, and evaluation metrics are specified. In this case, the categorical crossentropy loss function is used for multi-class classification. The Adam optimizer with a learning rate of 0.001 is employed for optimization. Additionally, various evaluation metrics such as accuracy, mean Intersection over Union (IoU), Dice coefficient, precision, sensitivity, specificity, and specific Dice coefficients for individual tumor regions are included to assess the model's performance across different aspects of segmentation quality.

```bash
      model.compile(
         loss="categorical_crossentropy",
         optimizer=keras.optimizers.Adam(learning_rate=0.001),
         metrics=[
            'accuracy', 
            tf.keras.metrics.MeanIoU(num_classes=4), 
            dice_coef, 
            precision, 
            sensitivity, 
            specificity, 
            dice_coef_necrotic, 
            dice_coef_edema, 
            dice_coef_enhancing
         ]
      )
```      
These steps ensure that the UNet model is properly constructed and configured for training, with appropriate loss and evaluation metrics to monitor its performance during training and evaluation phases.

## Contribution
- Richitha Dayara
- Goutham Senapathi
- KrinalbenMonpara
- Jamalaiah Sola

## Results

### Evaluation on Test Data

- **Loss:** 0.06
- **Accuracy:** 98.50%
- **Mean IoU:** 37.56%
- **Dice Coefficient:** 28.04%
- **Precision:** 98.48%
- **Sensitivity:** 98.48%
- **Specificity:** 99.49%
- **Dice Coefficient (Necrotic):** 9.30%
- **Dice Coefficient (Edema):** 20.62%
- **Dice Coefficient (Enhancing):** 5.20%

### Test Loss and Test Accuracy:
- **Test Loss:** 0.06
- **Test Accuracy:** 98.50%
- **Test Mean IoU:** 37.56%
- **Test Dice Coefficient:** 28.04%
- **Test Precision:** 98.48%
- **Test Sensitivity:** 98.48%
- **Test Specificity:** 99.49%
- **Test Dice Coefficient (Necrotic):** 9.30%
- **Test Dice Coefficient (Edema):** 20.62%
- **Test Dice Coefficient (Enhancing):** 5.20%



## Licenses
This project is not open for public use. It is part of a college project and is intended for educational purposes only. All rights reserved.
