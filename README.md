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

### Index calculation

#### Morphological indices

- **a-wave**: early systole positive wave
- **b-wave**: early systole negative wave
- **c-wave**: late systole reincreasing wave
- **d-wave**: late systole redecreasing wave
- **e-wave**: early distole pozitive wave
- **Pulse transit time (PTT)**: time between systole and diastole peaks
- **Large artery stiffness index (SI)**: height/PTT
- **Reflection Index (RI)**: b/a * 100
- **Dicrotic Notch Index**: *unknown*
- **Systolic slope inclination (alpha)**: steepest slope of the incresing wave
- **b/a**: Increased by CVD risk factors
- **d/a**: Decreased by CVD risk factors
- **Ageing index**: *unknown*
- **c-d point detection rate**: C and D wave detection ratio
- **Systolic-diastolic time ratio**: ratio of systolic and diastolic time
- **Ejection duration (ED)**: *unknown*
- **Left ventricular ejection time index (LVETI)(male)**: (1,7 * heart rate) + ED
- **Left ventricular ejection time index (LVETI)(female)**: (1,6 * heart rate) + ED
- **Ejection time @ 60**: ejection time adjusted for a pulse of 60/min (from start of period to the dicrotic notch)
- **Crest time @ 60**: time from the start of the period to the systole amplitude adjusted for a pulse of 60/min
- **ELVET 1 @ 60**: *"During ELVET 1 time, the heart does not have to deal with the retroactive force of the afterload"* adjusted for a pulse of 60/min
- **ELVET2 @ 60**: *"In the case of ELVET2, the afterload can already play a significant role in shaping the length of this time interval"* adjusted for a pulse of 60/min

#### Heart rate indices
- **SDNN**: Standard deviation of period lengths
- **rMSSD**: *unknown*
- **Total power**: Area under frequency domain
- **LF/HF**: The ratio of extreme values in the frequency domain
- **DFA Alpha 1**: *unknown*
