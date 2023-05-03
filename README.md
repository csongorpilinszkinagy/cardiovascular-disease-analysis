# Cardivascular disease (CVD) analysis

Pulse oximetry is a non-invasive method of measuring blood oxygen saturation (SpO2) levels, and it can also be used to calculate pulse rate. Recent studies have suggested that pulse oximeter data analysis can be used to predict the risk of cardiovascular diseases (CVDs) non-invasively. By analyzing the waveform data collected by a pulse oximeter, researchers have found that changes in the shape of the waveform can indicate early signs of CVDs such as arterial stiffness and endothelial dysfunction. In addition, pulse oximeter data can also provide information on heart rate variability, which is a strong predictor of CVDs. Therefore, the analysis of pulse oximeter data may offer a simple, cost-effective and non-invasive method for predicting the risk of CVDs in patients.

## Data source

Source: https://www.kaggle.com/mkachuee/BloodPressureDataset

There are three types of data:
* PPG: Photoplethysmogram (pulse oximeter data)
* ABP: Arterial blood pressure (invasive)
* ECG: Electrocadiogram

The whole dataset is in MAT format but there are also smaller segments in CSV.

Data stats:
* 5 GB of data
* 125Hz sampling frequency
* 61,000 sampling points/measurement
* 500 measurements in CSV format
* 12*1000 measurements in MAT format

## PPG analysis

### Data cleaning
In order to detects CVDs, feature extrantion is needed on the photoplethysmogram data. This relies on detecting local minima and maxima on the derivatives of the seuqences. Low frequency noise is due to the accidental movements during measurement, while high frequency noise is from electromagnetic disturbances during recording. Since the derivatives are highly sensitive to noise, the data needs cleaning both from low and high frequency noises. Fortunately the typical heart rate range is well defined. There are several ways to filter out noise:
- Fourier transform
- SVD
- PD-SVD
- Compressive sensing
- Sparsity transform
- Wavelet transform

### Segmentation
Finding local minima and maxima, then segmentation
https://www.researchgate.net/publication/299593684_An_innovative_peak_detection_algorithm_for_photoplethysmography_signals_An_adaptive_segmentation_method

### Segment aggregation
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3747602/

### Characteristic point detection
