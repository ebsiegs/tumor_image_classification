# Classifying Tumors in Mammograms

## Problem Statement

Breast Cancer is the second leading cause of death in women around the globe. Early detection through routine mammograms is the best prevention in improving Breast Cancer outcomes. 

For this project, we used 2 different mammogram datasets of differing sizes and built various neural network models in order to classify Tumors vs. No Tumors in mammogram images. Manual visual analysis of these images can be time consuming and subjective. This model aims to be used as a supplementary detection method for use by radiologists and oncologists.

## Executive Summary

## Project Workflow

### Data Sourcing, Cleaning, EDA & Data Augmentation
Searched for labeled mammogram image datasets. In this step we extracted our images, chose our classification of Tumor/No Tumor, explored the distribution of classifications and features, and prepared our datasets for modeling. Data Augmentation was also utlized for image simplification with the use of bounding box calculations and region of interest (ROI) preprocessing.

#### MIAS Dataset [Source](http://peipa.essex.ac.uk/info/mias.html)
[Part_1A_MIAS_Dataset_Cleaning_&_EDA.ipynb](code/Part_1A_MIAS_Dataset_Cleaning_&_EDA.ipynb)

![mias_mask](images/mias_mask.png)

#### DDSM Datasets [Source](https://www.kaggle.com/skooch/ddsm-mammography)
[Part_2A_DDSM_Dataset_Cleaning_&_EDA.ipynb](code/Part_2A_DDSM_Dataset_Cleaning_&_EDA.ipynb)

![density_subtlety](images/ddsm_density_subtlety.png)

### Modeling & Analysis
#### MIAS Modeling
[Part_1B_MIAS_Base_CNN_Modeling.ipynb](code/Part_1B_MIAS_Base_CNN_Modeling.ipynb)
[Part_1C_MIAS_Mask_R-CNN_Modeling.ipynb](code/Part_1C_MIAS_Mask_R-CNN_Modeling.ipynb)

![mias_model](images/mias_model.png)

#### DDSM Modeling
[Part_2B_DDSM_Modeling_&_Conclusions.ipynb](code/Part_1C_MIAS_Mask_R-CNN_Modeling.ipynb)

Beat Baseline with 92-93% accuracy on Test and Validation datasets

![ddsm_model](images/ddsm_model.png)

## Conclusions & Recommendations
- Using ML for tumor/no tumor image classification is a useful approach, however, it is not without its challenges!
- Larger training datasets improve accuracy and reduce overfitting
- Be careful of data leakage! Always do your train test split before any image augmentation. 
- With more time and further learning, there are a few more  image processing techniques and ML models to try in taking this work further.

## References
1. MIAS Data Source: http://peipa.essex.ac.uk/info/mias.html
2. DDSM Data Source: https://www.kaggle.com/skooch/ddsm-mammography
3. CBIS-DDSM Data Source (EDA): https://wiki.cancerimagingarchive.net/display/Public/CBIS-DDSM
3. https://www.kaggle.com/kmader/mias-mammography
4. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5954872/
5. https://pubmed.ncbi.nlm.nih.gov/24209932/
6. https://core.ac.uk/download/pdf/21748057.pdf
7. https://www.nature.com/articles/sdata2017177
