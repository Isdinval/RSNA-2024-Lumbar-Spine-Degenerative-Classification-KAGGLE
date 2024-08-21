# RSNA-2024-Lumbar-Spine-Degenerative-Classification-KAGGLE
Classify lumbar spine degenerative conditions

![header](https://github.com/user-attachments/assets/64805055-afa7-4b6a-ba1f-e6218a0b4b69)


## Overview
The goal of this competition is to create models that can be used to aid in the detection and classification of degenerative spine conditions using lumbar spine MR images. Competitors will develop models that simulate a radiologist's performance in diagnosing spine conditions.

## Description
Low back pain is the leading cause of disability worldwide, according to the World Health Organization, affecting 619 million people in 2020. Most people experience low back pain at some point in their lives, with the frequency increasing with age. Pain and restricted mobility are often symptoms of spondylosis, a set of degenerative spine conditions including degeneration of intervertebral discs and subsequent narrowing of the spinal canal (spinal stenosis), subarticular recesses, or neural foramen with associated compression or irritations of the nerves in the low back.

Magnetic resonance imaging (MRI) provides a detailed view of the lumbar spine vertebra, discs, and nerves, enabling radiologists to assess the presence and severity of these conditions. Proper diagnosis and grading of these conditions help guide treatment and potential surgery to help alleviate back pain and improve overall health and quality of life for patients.

RSNA has teamed with the American Society of Neuroradiology (ASNR) to conduct this competition exploring whether artificial intelligence can be used to aid in the detection and classification of degenerative spine conditions using lumbar spine MR images.

The challenge will focus on the classification of five lumbar spine degenerative conditions: Left Neural Foraminal Narrowing, Right Neural Foraminal Narrowing, Left Subarticular Stenosis, Right Subarticular Stenosis, and Spinal Canal Stenosis. For each imaging study in the dataset, we’ve provided severity scores (Normal/Mild, Moderate, or Severe) for each of the five conditions across the intervertebral disc levels L1/L2, L2/L3, L3/L4, L4/L5, and L5/S1.

To create the ground truth dataset, the RSNA challenge planning task force collected imaging data sourced from eight sites on five continents. This multi-institutional, expertly curated dataset promises to improve standardized classification of degenerative lumbar spine conditions and enable the development of tools to automate accurate and rapid disease classification.

Challenge winners will be recognized at an event during the RSNA 2024 annual meeting. For more information on the challenge, contact RSNA Informatics staff at informatics@rsna.org.

![3img](https://github.com/user-attachments/assets/229cc15e-373b-4ea0-8516-3cf7abbe0183)


## Evaluation
Submissions are evaluated using the average of sample weighted log losses and an any_severe_spinal prediction generated by the metric. The metric notebook can be found here.

The sample weights are as follows:
1 for normal/mild.
2 for moderate.
4 for severe.
For each row ID in the test set, you must predict a probability for each of the different severity levels. The file should contain a header and have the following format:

| row_id | normal_mild | moderate | severe |
| --- | --- | --- | --- |
| '123456_left_neural_foraminal_narrowing_l1_l2' | 0.333 | 0.333 | 0.333 |
| '123456_left_neural_foraminal_narrowing_l2_l3' | 0.333 | 0.333 | 0.333 |
| '123456_left_neural_foraminal_narrowing_l3_l4' | 0.333 | 0.333 | 0.333 |
etc.

## Dataset Description
The goal of this competition is to identify medical conditions affecting the lumbar spine in MRI scans.

This competition uses a hidden test. When your submitted notebook is scored, the actual test data (including a full-length sample submission) will be made available to your notebook.

### Files
#### train.csv Labels for the train set.
- study_id - The study ID. Each study may include multiple series of images.
[condition]_[level] - The target labels, such as spinal_canal_stenosis_l1_l2, with the severity levels of Normal/Mild, Moderate, or Severe. Some entries have incomplete labels.
train_label_coordinates.csv
- study_id
- series_id - The imagery series ID.
- instance_number - The image's order number within the 3D stack.
- condition - There are three core conditions: spinal canal stenosis, neural_foraminal_narrowing, and subarticular_stenosis. The latter two are considered for each side of the spine.
- level - The relevant vertebrae, such as l3_l4
- [x/y] - The x/y coordinates for the center of the area that defines the label.

#### sample_submission.csv
- row_id - A slug of the study ID, condition, and level such as 12345_spinal_canal_stenosis_l3_l4.
- [normal_mild/moderate/severe] - The three prediction columns.

#### [train/test]_images/[study_id]/[series_id]/[instance_number].dcm The imagery data.
#### [train/test]_series_descriptions.csv
- study_id
- series_id
- series_description The scan's orientation.

## NOTEBOOKS
**anatomy-image-visualization-overview-rsna-raids.ipynb**

This notebook aims to give a brief overview of the data available in the RSNA-RAIDS challenge and how to visualize some of the conditions in the dataset (**Original notebook by Abhinav Suri** provided at the beginning of the competition).
In this notebook, we cover:
* The basic distribution of cases in the population
* How to identify which scans and diagnoses correspond to each patient
* How to visualize patient DICOMs and locations of annotated pathologies

**anatomy-image-visualization-overview-rsna-raids.ipynb**

This notebook aims to convert DICOM images from the RSNA 2024 Lumbar Spine Degenerative Classification dataset into PNG format for further processing.
In this notebook, we cover:
* Reads CSV files containing image metadata.
* Iterates over study IDs and series descriptions.
* Loads DICOM images for each series.
* Preprocesses images (normalization, resizing).
* Saves preprocessed images as PNG files.

**OUTPUT** : 16 GB of PNG images have been created.

