# Exoplanet Detection: Analyzing Kepler Space Telescope Flux Data

## Project Summary

In this project, we aimed to detect exoplanets (or "exostars") using flux measurements from the Kepler Space Telescope. Our goal was to classify stars based on their light curves—specifically, to distinguish between stars that host exoplanets and those that do not. Given the severe imbalance in the dataset (with very few exoplanet-hosting stars), we experimented with several machine learning models and resampling techniques to improve detection.

Our modeling pipeline began with a baseline logistic regression and advanced through a neural network, XGBoost, and Random Forest. These models were compared using metrics such as precision, recall, F1-score, and ROC-AUC, with particular focus on detecting the rare exoplanet instances.

## Problem Statement

The task is to identify exoplanets from Kepler Space Telescope data by analyzing time-series flux measurements. Exoplanet detection is challenging because the planetary transit signal is subtle and embedded in noisy data influenced by stellar variability and instrumental artifacts. Our objective is to build a model that can reliably detect the slight, periodic dimming of a star when a planet transits across its face.

### Complete Statement of the Problem

- **Goal:** Detect the subtle dimming in stellar flux caused by transiting exoplanets.
- **Challenges:**  
  - **Extreme class imbalance:** Very few stars are confirmed to host exoplanets.
  - **Noisy data:** Variability from the stars and measurement noise complicate the signal.
  - **Subtle signals:** The transit-induced dip in brightness is often very small.
  
Our approach involves resampling techniques to balance the data and the use of multiple models to evaluate performance beyond overall accuracy.

## Benchmark & Evaluation Metrics

Due to the imbalanced nature of the dataset, overall accuracy is misleading. We benchmark our models using:
- **Precision:** The proportion of predicted exoplanets that are correct.
- **Recall:** The proportion of actual exoplanets that are detected.
- **F1-Score:** The harmonic mean of precision and recall.
- **ROC-AUC:** Measures the trade-off between true positive and false positive rates.

These metrics allow us to better assess the performance in detecting the minority class (exoplanet-hosting stars).

## Data Source and Characteristics

The dataset is derived from NASA's Kepler mission and contains:

- **Training Set:**
  - **Instances:** 5,087 observations
  - **Attributes:** 3,198 features (1 label column + 3,197 flux measurements)
  - **Composition:** 37 confirmed exoplanet-hosting stars and 5,050 non-exoplanet stars
- **Test Set:**
  - **Instances:** 570 observations
  - **Attributes:** Same as training set
  - **Composition:** 5 confirmed exoplanet-hosting stars and 565 non-exoplanet stars

### Variables

- **LABEL:** Binary indicator where (after conversion) 0 denotes exoplanet-hosting and 1 denotes non-exoplanet stars (or vice versa as adjusted during preprocessing).
- **FLUX.1 to FLUX.3197:** Sequential flux measurements representing the star’s light intensity over time.

### Data Collection & Labeling

- **Source:** Data is sourced from the Kepler Space Telescope, which observes periodic dimming due to planetary transits.
- **Collection Process:** Flux measurements are recorded at regular intervals and later processed to detect transit signals.
- **Labeling:** Confirmed exoplanet detections have been validated through multiple observational methods and manual verification by astronomers.

## Exploratory Data Analysis (EDA)

Several EDA techniques were applied to understand the data:
- **Light Curve Visualization:** Line plots were used to compare the flux patterns of stars with and without detected exoplanets.
- **Outlier Detection:** Box plots helped identify extreme flux values that might impact model performance.
- **Autocorrelation & Fourier Analysis:** These methods were used to detect periodic patterns in the light curves.
- **Phase Folding:** This technique aligned potential transit events to enhance the visibility of periodic dips.

## Modeling Approach

We implemented and compared several models:

1. **Logistic Regression:**  
   - **Overview:** A simple, interpretable baseline.
   - **Results:** Achieved overall high accuracy (~99%) but only a 20% recall for exoplanets (F1 ≈ 0.25).

2. **Neural Network (NN):**  
   - **Overview:** A multi-layer deep learning model with dropout and regularization.
   - **Results:** Improved recall (≈60%) for exoplanets at the expense of extremely low precision, resulting in many false positives and a low F1-score for exoplanets.

3. **XGBoost:**  
   - **Overview:** A gradient-boosted tree model known for handling nonlinearities.
   - **Results:** Similar to logistic regression, with about 20% recall and F1-score of 0.25 for exoplanets.

4. **Random Forest:**  
   - **Overview:** An ensemble tree-based model with balanced class weights.
   - **Results:**  
     - **Precision for exoplanets:** 1.00 (perfect when predicting an exoplanet)
     - **Recall for exoplanets:** 0.20 (detects only 20% of exoplanets)
     - **F1-Score for exoplanets:** 0.33  
     Although the overall accuracy was 99%, the recall remains low, meaning the model is very conservative in predicting exoplanets.

## Final Observations

- **Performance Trade-offs:**  
  - Logistic Regression, XGBoost, and Random Forest all exhibit similar behavior—very high overall accuracy dominated by the majority class, but very low recall for exoplanets.
  - The neural network model increased recall, but with an unacceptable drop in precision.
- **Challenge:**  
  The key challenge remains the extreme imbalance and subtle signal of exoplanets. The models tend to favor the majority class, leading to a high rate of missed detections.
  
## Running the Project

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Entropyxz/Exoplanet-Hunt
   cd exoplanet-hunt
