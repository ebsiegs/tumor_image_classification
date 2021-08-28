# Classifying Tumors in Mammograms

## Problem Statement

Breast Cancer is the second leading cause of death in women around the globe. Early detection through routine mammograms is the best prevention in improving Breast Cancer outcomes. 

For this project, we used 2 different mammogram datasets of differing sizes and built various neural network models in order to classify Tumors vs. No Tumors in mammogram images. Manual visual analysis of these images can be time consuming and subjective. This model aims to be used as a supplementary detection method for use by radiologists and oncologists.

## Executive Summary

The two different datasets used, [MIAS](http://peipa.essex.ac.uk/info/mias.html) and [CBIS-DDSM](https://www.kaggle.com/skooch/ddsm-mammography), were used to try and tackle the issue of using neural networks to identify tumors. The MIAS dataset had 332 images and the CBIS-DDSM set had over 60k+ images. The MIAS dataset had clear classifications, bounding boxes, and supplementary information for creating clear categories, but its small number of images proved limiting in the ability to do better than base. On the other hand, the CBIS-DDSM dataset had ample images to choose from, but the dataset was not the clearest. 

The MIAS dataset was cleaned and various attempts at a CNN and classification was made. Classifications were attempted at whether a tumor was present, as well as type of tumor. Neither of the forms of classifications yielded good results for the dataset. Many different approaches for a CNN was attempted, with the following variables altered:
 - Number and size of hidden Convolution layers (1 to 4 layers, 10-128 filters)
 - Number and size Dense Layers (1-5 dense layers, 120-2000 nodes)
 - Various forms of regularization (L1,Batch, and Dropout)
 - Image size (100x100-1024x1024 pixels)
 - Rotations

The accuracy topped out for the MIAS Dataset at 70%, which was more a result of fluctuations as the training set became overtrained. Baseline of guessing all non-tumor was maintained until the training set began to overtrain, and then in the validation set the more tumors would be predicted at nominal success. Changing image size had varying success, and smaller images resulted in more consistent results. 

A different approach of seeing if a Mask RCNN could potentially correctly make masks for tumors to some success. Using a [tutorial](https://machinelearningmastery.com/how-to-train-an-object-detection-model-with-keras/) and a [forked version](https://github.com/ahmedfgad/Mask-RCNN-TF2) of the package was used. A dataset class was made for the mammograms, with two classifications, normal and tumor made, where a dummy bounding box of 0 pixels was made for the normal class. This performed well in some instances, alright in others, and poorly or not at all in the rest. The IoU was not calculated because the success rate was not high enough or consistent enough to consider it.

The CBIS-DDSM dataset was preprocessed before download, and most of the techniques attempted on MIAS could translate to here. The same fitting techniques were performed on this dataset, with the difference in maximum image size being limited to 299x299.  Smaller images again fit better on the validation set, most likely due to the model over training on image specific details, which was lost in the validation set. A separate validation set was used compared to the train-test set used for model evaluation. Most models achieved over 90% accuracy from the baseline of 87% on the separate validation set, with the best performing model reaching 93.1% accuracy and 92.1% f1-score. Without using more robust measures this was the limit of what we could achieve. 


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

Conclusions:

The DDSM model was able to beat the baseline accuracy of 87% by 5% using the preprocessed images in the CBIS-DDSM data set.  While this model is a step in the correct direction, it may yet be accurate enough to help oncologists correctly identify tumors.  Another point of concern is the model has a high rate of providing false negatives, a particularly dangerous failure mode in such a model.  With additional work, these models can be a good first step in the quest for higher accuracy tumor identification models.

The Mask R-CNN model on the MIAS data set while sometimes able to accurately apply a bounding box to tumors, was unreliable in its capability to detect tumors, based on a review of prediction images.  Potentially on a larger data set, such as the DDSM dataset, Mask R-CNN will yield better consistency

Recommendations:

With complex images like this a large data set, such as the DDSM is needed.  Generating models that could beat the baseline on the MIAS dataset of 322 images was difficult without overfitting the model. 

Running these images through a CNN is resource intensive.  With additional computing power and models that resist overfitting, the full image could be fed through without downsizing giving the model a chance to detect smaller tumors.

Additional clarification on the pre-processing done to the DDSM image set would help understand the value of the set.  Understanding how rotated images and copies of images was done would help clear assurances there is no data leakage between validation and train sets.

Additional image manipulation may give the model a better chance to fit, and is an avenue to continue to look down.

With the complexity of the issue, working alongside an expert in mammography and oncology is critical.  The addition of metadata may yield additional accuracy.  Another approach may be to not just look at each mammograph in isolation, but in a time series per patient.


## References
1. MIAS Data Source: http://peipa.essex.ac.uk/info/mias.html
2. DDSM Data Source: https://www.kaggle.com/skooch/ddsm-mammography
3. CBIS-DDSM Data Source (EDA): https://wiki.cancerimagingarchive.net/display/Public/CBIS-DDSM
3. https://www.kaggle.com/kmader/mias-mammography
4. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5954872/
5. https://pubmed.ncbi.nlm.nih.gov/24209932/
6. https://core.ac.uk/download/pdf/21748057.pdf
7. https://www.nature.com/articles/sdata2017177
