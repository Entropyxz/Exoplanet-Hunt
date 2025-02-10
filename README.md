# Exoplanet Detection: Analyzing Kepler Space Telescope Flux Data

## Project Summary

In this project, we aimed to detect exoplanets (or "exostars") using flux measurements from the Kepler Space Telescope. Our goal was to classify stars based on their light curves—specifically, to distinguish between stars that host exoplanets and those that do not. Given the severe imbalance in the dataset (with very few exoplanet-hosting stars), we experimented with several machine learning models and resampling techniques to improve detection.

Our modeling pipeline began with a baseline logistic regression and advanced through a neural network. These models were compared using metrics such as precision, recall, F1-score, and ROC-AUC, with particular focus on detecting the rare exoplanet instances.

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

  
## Running the Project

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Entropyxz/Exoplanet-Hunt
   cd exoplanet-hunt
