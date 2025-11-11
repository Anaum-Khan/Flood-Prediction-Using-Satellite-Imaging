# Flood Prediction for River Gomti Using Satellite Imagery

[cite_start]This repository contains the minor project "Flood Prediction Using Satellite Imagery: River Gomti"[cite: 11, 12, 13], completed by Anaum Khan and Mohd. [cite_start]Yousuf Waseem under the supervision of Prof. Saiful Islam[cite: 4, 7, 9].

The project focuses on creating a model to predict binary flood risk (flood or no-flood) by analyzing meteorological data and satellite imagery.

## Motivation

[cite_start]Floods are among the most devastating natural disasters, causing significant loss of life and property[cite: 74]. [cite_start]The state of Uttar Pradesh is particularly vulnerable due to its major river systems, including the Ganga, Yamuna, and Gomti[cite: 75, 77]. [cite_start]The low-lying regions surrounding the Gomti River are frequently inundated during monsoons, disrupting millions of lives[cite: 78, 79].

[cite_start]This project aims to leverage data-driven methods for localized risk assessment and to support disaster management efforts[cite: 93, 99].

## Methodology

The project follows a comprehensive workflow from data collection to model deployment.

### 1. Data Collection

We collected data from two primary sources:

* [cite_start]**Google Earth Engine (GEE) API**[cite: 135]:
    * [cite_start]**Rainfall:** 'UCSB-CHG/CHIRPS/DAILY' dataset[cite: 141].
    * [cite_start]**Temperature & Humidity:** 'ECMWF/ERA5_LAND/HOURLY' dataset[cite: 146, 152].
* [cite_start]**Sentinel-2 Satellite Imagery**[cite: 156]:
    * [cite_start]Used to derive **NDVI (Normalized Difference Vegetation Index)**[cite: 165].
    * [cite_start]Used to derive **Water Index**[cite: 159].

### 2. Data Preprocessing

The collected data was processed to create a robust, tabular dataset for training our machine learning models.

* [cite_start]**Feature Engineering:** Created features like `average_rainfall_mm`, `average_temperature_C`, `average_humidity_c`, `soil_moisture_0_7cm_percentage`, `rainfall_3day`, and `rainfall_7day`[cite: 184].
* **Risk Index Calculation:** We defined a custom **Risk Index** to quantify the flood threat:
    > [cite_start]`Risk Index = (0.6 * Normalized 3-day Rainfall) + (0.4 * Normalized Soil Moisture)` [cite: 200, 205, 206]
* [cite_start]**Thresholding:** The continuous `Risk Index` was categorized into five levels (No Risk, Low, Moderate, High, Very High) [cite: 193-198] [cite_start]and then converted into a final `flood_risk_binary` (0 for No Risk, 1 for any level of risk)[cite: 199, 217, 220].
* **Balancing Data:** The initial dataset was imbalanced. [cite_start]We applied **SMOTE (Synthetic Minority Over-sampling Technique)** to create a balanced dataset for training, preventing model bias[cite: 254, 267].

## Models & Results

We explored both deep learning and classical machine learning models. The ML models were trained on the preprocessed tabular data, while the DL models were trained on image data for comparison.

### Machine Learning Models

The models trained on the feature-engineered, SMOTE-balanced data showed outstanding performance:

| Model | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: |
| **XGBoost Classifier** | **100.0%** | **100.0%** | [cite_start]**100.0%** | [cite: 272]
| **Random Forest Classifier** | 89.0% | 93.0% | [cite_start]91.0% | [cite: 272]
| **Support Vector Classifier (SVC)** | 89.0% | 93.0% | [cite_start]91.0% | [cite: 272]

[cite_start]The **XGBoost Classifier** was the best-performing model, achieving perfect scores on the test data[cite: 272, 276].

### Deep Learning Models (Comparative)

| Model | Class | Precision | Recall | F1-Score | Accuracy |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **ResNet50** | `flood_images` | 0.75 | 0.43 | 0.55 | **0.75** |
| | `non_flood_images` | 0.75 | 0.92 | 0.83 | |
| **VGG16** | `flood_images` | 0.45 | 0.71 | 0.56 | **0.60** |
| | `non_flood_images` | 0.78 | 0.54 | 0.64 | |

While the ML models excelled, the ResNet50 model also showed decent (75%) accuracy in classifying raw images.

## Future Work

We plan to extend this project in several ways:

1.  [cite_start]**Data Enhancement:** Utilize higher-resolution spatial and temporal datasets for more granular predictions[cite: 279].
2.  [cite_start]**Model Improvement:** Implement ensemble methods combining the best of our ML and DL models for more robust predictions[cite: 280].
3.  [cite_start]**Deployment:** Develop an interactive dashboard for real-time visualization and decision-making to aid local authorities[cite: 281].
4.  [cite_start]**Validation:** Collaborate with stakeholders for on-ground validation and integration into early warning systems[cite: 282].

## Project Authors

* [cite_start]**Anaum Khan** (22COB307) [cite: 7, 8]
* **Mohd. [cite_start]Yousuf Waseem** (22COB407) [cite: 9, 10]

### Supervisor
* **Prof. [cite_start]Saiful Islam** [cite: 4]
