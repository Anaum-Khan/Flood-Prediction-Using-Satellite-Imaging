# Flood Prediction for River Gomti Using Satellite Imagery

This repository contains the minor project "Flood Prediction Using Satellite Imagery: River Gomti", completed by Anaum Khan and Mohd. Yousuf Waseem under the supervision of Prof. Saiful Islam.

The project focuses on creating a model to predict binary flood risk (flood or no-flood) by analyzing meteorological data and satellite imagery.

## Motivation

Floods are among the most devastating natural disasters, causing significant loss of life and property. The state of Uttar Pradesh is particularly vulnerable due to its major river systems, including the Ganga, Yamuna, and Gomti. The low-lying regions surrounding the Gomti River are frequently inundated during monsoons, disrupting millions of lives.

This project aims to leverage data-driven methods for localized risk assessment and to support disaster management efforts.

## Methodology

The project follows a comprehensive workflow from data collection to model deployment.

### 1. Data Collection

We collected data from two primary sources:

* **Google Earth Engine (GEE) API**:
    * **Rainfall:** 'UCSB-CHG/CHIRPS/DAILY' dataset.
    * **Temperature & Humidity:** 'ECMWF/ERA5_LAND/HOURLY' dataset.
* **Sentinel-2 Satellite Imagery**:
    * Used to derive **NDVI (Normalized Difference Vegetation Index)**.
    * Used to derive **Water Index**.

### 2. Data Preprocessing

The collected data was processed to create a robust, tabular dataset for training our machine learning models.

* **Feature Engineering:** Created features like `average_rainfall_mm`, `average_temperature_C`, `average_humidity_c`, `soil_moisture_0_7cm_percentage`, `rainfall_3day`, and `rainfall_7day`.
* **Risk Index Calculation:** We defined a custom **Risk Index** to quantify the flood threat:
    > `Risk Index = (0.6 * Normalized 3-day Rainfall) + (0.4 * Normalized Soil Moisture)`
* **Thresholding:** The continuous `Risk Index` was categorized into five levels (No Risk, Low, Moderate, High, Very High) and then converted into a final `flood_risk_binary` (0 for No Risk, 1 for any level of risk).
* **Balancing Data:** The initial dataset was imbalanced. We applied **SMOTE (Synthetic Minority Over-sampling Technique)** to create a balanced dataset for training, preventing model bias.

## Models & Results

We explored both deep learning and classical machine learning models. The ML models were trained on the preprocessed tabular data, while the DL models were trained on image data for comparison.

### Machine Learning Models

The models trained on the feature-engineered, SMOTE-balanced data showed outstanding performance:

| Model | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: |
| **XGBoost Classifier** | **100.0%** | **100.0%** | **100.0%** |
| **Random Forest Classifier** | 89.0% | 93.0% | 91.0% |
| **Support Vector Classifier (SVC)** | 89.0% | 93.0% | 91.0% |

The **XGBoost Classifier** was the best-performing model, achieving perfect scores on the test data.

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

1.  **Data Enhancement:** Utilize higher-resolution spatial and temporal datasets for more granular predictions.
2.  **Model Improvement:** Implement ensemble methods combining the best of our ML and DL models for more robust predictions.
3.  **Deployment:** Develop an interactive dashboard for real-time visualization and decision-making to aid local authorities.
4.  **Validation:** Collaborate with stakeholders for on-ground validation and integration into early warning systems.

## Project Authors

* **Anaum Khan** (22COB307)
* **Mohd. Yousuf Waseem** (22COB407)

### Supervisor
* **Prof. Saiful Islam**
