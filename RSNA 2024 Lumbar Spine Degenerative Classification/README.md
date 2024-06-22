# [Competition](https://www.kaggle.com/competitions/rsna-2024-lumbar-spine-degenerative-classification/overview)
## Overview
The goal of this competition is to create models that can be used to aid in the detection and classification of degenerative spine conditions using lumbar spine MR images. Competitors will develop models that simulate a radiologist's performance in diagnosing spine conditions.

## Description
Low back pain is the leading cause of disability worldwide, according to the World Health Organization, affecting 619 million people in 2020. Most people experience low back pain at some point in their lives, with the frequency increasing with age. Pain and restricted mobility are often symptoms of spondylosis, a set of degenerative spine conditions including degeneration of intervertebral discs and subsequent narrowing of the spinal canal (spinal stenosis), subarticular recesses, or neural foramen with associated compression or irritations of the nerves in the low back.

Magnetic resonance imaging (MRI) provides a detailed view of the lumbar spine vertebra, discs and nerves, enabling radiologists to assess the presence and severity of these conditions. Proper diagnosis and grading of these conditions help guide treatment and potential surgery to help alleviate back pain and improve overall health and quality of life for patients.

RSNA has teamed with the American Society of Neuroradiology (ASNR) to conduct this competition exploring whether artificial intelligence can be used to aid in the detection and classification of degenerative spine conditions using lumbar spine MR images.

The challenge will focus on the classification of five lumbar spine degenerative conditions: Left Neural Foraminal Narrowing, Right Neural Foraminal Narrowing, Left Subarticular Stenosis, Right Subarticular Stenosis, and Spinal Canal Stenosis. For each imaging study in the dataset, we’ve provided severity scores (Normal/Mild, Moderate, or Severe) for each of the five conditions across the intervertebral disc levels L1/L2, L2/L3, L3/L4, L4/L5, and L5/S1.

To create the ground truth dataset, the RSNA challenge planning task force collected imaging data sourced from eight sites on five continents. This multi-institutional, expertly curated dataset promises to improve standardized classification of degenerative lumbar spine conditions and enable development of tools to automate accurate and rapid disease classification.

Challenge winners will be recognized at an event during the RSNA 2024 annual meeting. For more information on the challenge, contact RSNA Informatics staff at informatics@rsna.org.


# [Data](https://www.kaggle.com/competitions/rsna-2024-lumbar-spine-degenerative-classification/data)
The goal of this competition is to identify medical conditions affecting the lumbar spine in MRI scans.

This competition uses a hidden test. When your submitted notebook is scored, the actual test data (including a full length sample submission) will be made available to your notebook.

## Files
### train.csv Labels for the train set.

* study_id - The study ID. Each study may include multiple series of images.
* [condition]_[level] - The target labels, such as spinal_canal_stenosis_l1_l2, with the severity levels of Normal/Mild, Moderate, or Severe. Some entries have incomplete labels.

### train_label_coordinates.csv
* study_id
* series_id - The imagery series ID.
* instance_number - The image's order number within the 3D stack.
* condition - There are three core conditions: spinal canal stenosis, neural_foraminal_narrowing, and subarticular_stenosis. The latter two are considered for each side of the spine.
* level - The relevant vertebrae, such as l3_l4
* [x/y] - The x/y coordinates for the center of the area that defined the label.
### sample_submission.csv
* row_id - A slug of the study ID, condition, and level such as 12345_spinal_canal_stenosis_l3_l4.
* [normal_mild/moderate/severe] - The three prediction columns.
### [train/test]_images/[study_id]/[series_id]/[instance_number].dcm The imagery data.

### [train/test]_series_descriptions.csv

* study_id
* series_id
* series_description The scan's orientation.

# Visualization
Since this is a image classification competition, a good visualization could help us better understand the objectives. I added a [visualization notebook](https://www.kaggle.com/code/abhinavsuri/anatomy-image-visualization-overview-rsna-raids).

# Model
## RSNA2024 LSDC Training DenseNet
This notebook is forked [here](https://www.kaggle.com/code/itsuki9180/rsna2024-lsdc-training-baseline). In the [previous notebook](https://www.kaggle.com/code/itsuki9180/rsna2024-lsdc-making-dataset), the author selected the images we wanted to use and exported them to png.The original notebook training. And the original other trained EfficientNet_B4 model with these images. 

I desided to change the model to see if there is any improvement. The reason why I choose DenseNet201 for training is that DenseNet201 has generally same number of parameters and size with EfficientNet_B4 so that I believe that Kaggle GPU could handle it and we don't need extra machine.

### Credit
- [RSNA2024 LSDC Making Dataset](https://www.kaggle.com/code/itsuki9180/rsna2024-lsdc-making-dataset) 
- [RSNA2024 LSDC Training DenseNet](https://www.kaggle.com/code/hugowjd/rsna2024-lsdc-training-densenet) <- you're reading now
- [RSNA2024 LSDC Submission DenseNet](https://www.kaggle.com/code/itsuki9180/rsna2024-lsdc-submission-baseline)

### Reference:
* [Huang, G., Liu, Z., Van Der Maaten, L., and Weinberger, K. Q. Densely connected convolutional networks. CVPR, 2017.](https://arxiv.org/abs/1608.06993)
* [Mingxing Tan and Quoc V. Le. EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks. ICML 2019.](https://arxiv.org/abs/1905.11946)

### Future Improvement
* I'm certain that we can run other models to train these images. We can do it by changing ***MODEL_NAME*** parameters in **Config** session. I would list some CNN models which are suitable for image classification and these numbers of parameters.
  * ResNet:
    * ResNet-18: ~11.7 million parameters
    * **ResNet-34: ~21.8 million parameters**
    * **ResNet-50: ~25.6 million parameters**
    * ResNet-101: ~44.5 million parameters
    * ResNet-152: ~60 million parameters
  * VGG:
    * VGG-16: ~138 million parameters
    * VGG-19: ~143 million parameters
  * Inception Networks:
    * Inception v1 (GoogleNet): ~6.8 million parameters
    * Inception v3: ~23.8 million parameters
  * DenseNet:
    * DenseNet-121: ~8 million parameters
    * **DenseNet-169: ~14 million parameters**
    * **DenseNet-201: ~20 million parameters**
    * DenseNet-264: ~33 million parameters
  * MobileNets (parameters can vary significantly with changes in alpha and resolution multipliers):
    * MobileNetV1 (1.0 224): ~4.2 million parameters
    * MobileNetV2 (1.0 224): ~3.5 million parameters
    * MobileNetV3 Large: ~5.4 million parameters
  * Vision Transformers (ViT):
    * ViT-B/16 (base model with patch size 16x16): ~86 million parameters
  * Xception:
    * **Xception: ~22.9 million parameters**
  * EfficientNet
    * EfficientNet-B0: ~5.3 million parameters
    * EfficientNet-B1: ~7.8 million parameters
    * EfficientNet-B2: ~9.2 million parameters
    * EfficientNet-B3: ~12 million parameters
    * **EfficientNet-B4: ~19 million parameters**
    * EfficientNet-B5: ~30 million parameters
    * EfficientNet-B6: ~43 million parameters
    * EfficientNet-B7: ~66 million parameters
* The original author said that we can improve the dataset making process
* I only trained 5 **folds** and 10 **epochs**, you can modify these parameters. But take care of overfitting.

## Submission

The [original notebook](https://www.kaggle.com/code/itsuki9180/rsna2024-lsdc-submission-baseline) uses EfficientNet model and [my submission file](https://www.kaggle.com/code/hugowjd/rsna2024-lsdc-densenet-submission) changed it to DenseNet, using my own weights.


# Current Update
* 6/20/2024 - Combine 5 folds of EfficientNet and 5 folds of DenseNet -> LB score: 0.64
* 6/21/2024 - Trained 5 folds of Xception41, 10 epochs each -> LB score: 0.66