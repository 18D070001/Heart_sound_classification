# Heart_sound_classification

## Introduction

The 2016 PhysioNet/CinC Challenge aims to encourage the development of algorithms to classify heart sound recordings collected from a variety of clinical or nonclinical (such as in-home visits) environments. The aim is to identify, from a single short recording (10-60s) from a single precordial location, whether the subject of the recording should be referred on for an expert diagnosis.

During the cardiac cycle, the heart firstly generates the electrical activity and then the electrical activity causes atrial and ventricular contractions. This in turn forces blood between the chambers of the heart and around the body. The opening and closure of the heart valves is associated with accelerations-decelerations of blood, giving rise to vibrations of the entire cardiac structure (the heart sounds and murmurs) . These vibrations are audible at the chest wall, and listening for specific heart sounds can give an indication of the health of the heart. The phonocardiogram (PCG) is the graphical representation of a heart sound recording. 

## Dataset

The dataset used in this project is provided by 2016 Physionet/Cinc . 
Heart sound recordings we)re sourced from several contributors around the world, collected at either a clinical or nonclinical environment, from both healthy subjects and pathological patients. The Challenge training set consists of five databases (A through E) containing a total of 3,126 heart sound recordings, lasting from 5 seconds to just over 120 seconds. You can [browse these files](https://physionet.org/content/challenge-2016/#files)  , or download the entire training set as a zip archive (169 MB) .

### Files
Total uncompressed size: 1.1 GB.

Access the files
[Download the ZIP file](https://physionet.org/static/published-projects/challenge-2016/classification-of-heart-sound-recordings-the-physionet-computing-in-cardiology-challenge-2016-1.0.0.zip) (1011.4 MB)

Access the files using the Google Cloud Storage Browser [here](https://console.cloud.google.com/storage/browser/challenge-2016-1.0.0.physionet.org/)  . Login with a Google account is required.


Access the data using Google Cloud "gsutil": `gsutil -m cp -r gs://challenge-2016-1.0.0.physionet.org DESTINATION`
Download the files using your terminal: `wget -r -N -c -np https://physionet.org/files/challenge-2016/1.0.0/`


In each of the databases, each record begins with the same letter followed by a sequential, but random number. Files from the same patient are unlikely to be numerically adjacent. The training and test sets have each been divided so that they are two sets of mutually exclusive populations (i.e., no recordings from the same subject/patient were are in both training and test sets). Moreover, there are two data sets that have been placed exclusively in either the training or test databases (to ensure there are ‘novel’ recording types and to reduce overfitting on the recording methods). 

## About the project

### PROPOSED HYPOTHESIS

The current stethoscope is capable of recording heart sounds. The PCG signals obtained are
temporal sequences and thus can be modeled using sophisticated Recurrent Neural Networks.
Due to their well-known capabilities for modeling and analyzing sequential data even in the
presence of noise, we developed an RNN model for automated cardiac auscultation.


## PREPROCESSING
### Denoising
The denoising function) removes speech and ambient noise components from the PCG signal.
The current code has not used the above function but to improve classification accuracy and
manual hearing it is highly recommended to denoise the raw data

### Segmentation 

It is the process of identifying and extracting the discrete portions from the heart signal which
are S1 (Lub) and S2 (Dub). The main aim of this process is to align all audio data from a
common reference point (for ex. S1) and extract 2, 5 or 8 heart cycles that are required for the
RNN models’ enhanced performance.

The following methods were implemented for segmentation :

- Springer Segmentation algorithm : This algorithm is a probabilistic model that trains
an HMM model based on logistic regression to assign the various states of the parts of
the heart cycle(1-S1, 2-systole, 3-S2, 4-Diastole). The output is an array of assigned
states which gives us the segments i.e. cycles of the heart sound. This requires ECG
data for the corresponding PCG data for training the HMM. The Physionet dataset had
ECG data only for training-a and thus the algorithm performed poorly for the other data
sets.

- The wider the range of ECG available for the training data the better the
segmentation process.


- The current springer code is in Matlab which is slower and an implementation in
Python will be faster.



## FEATURE SELECTION

We used Mel-frequency cepstral coefficients (MFCCs) to represent the PCG signal in
compact representation. MFCCs are used almost in every study on automatic heart sound
classification due to their effectiveness in speech analysis. We compute MFCCs from 25ms of
the window with a step size of 10ms. We select the first 13 MFCCs for compact representation
of the PCG signal as a large feature space does not always improve the recognition rate of the
model.






## The Model

## RNN MODEL
### Model Structure:
- visible layer or input layer : size of input = 13 (mfcc matrix has column size 13)
- hidden layer 1: LSTM layer
- hidden layer 2: LSTM layer
- 1 dense layer having activation function = "relu" (rectified linear)
- output layer : classification  


### Building the Model:
- loss function: to compute the loss (currently "mean squared error")
- optimizer function: adam
- metrics: accuracy
- **model.fit:** this function tries for the best possible fit of the model to the training data.
<br>


### HYPER PARAMETERS
- Dropout : It is used for regularization(has to be tried for different values to find optimum
dropout)
- No. of LSTM layers: the trend showed that accuracy increased with increase in layers
but it also affected the computation significantly.

- Threshold for classification for 0/1. (has to be tried for different values to find optimum
threshold)


## CONCLUSION
- RNN provides promising results with accuracy close to 70%. Idealy First we should align S1/S2 segments to get best results. 

- The accuracy was increasing as the number of LSTM layers was increasing but resulted
in a significantly larger computation period.

- There is a tradeoff between sensitivity and specificity depending on the threshold for
classification.

**for better accuracy, first one may use [springer segmentation code](https://github.com/davidspringer/Springer-Segmentation-Code) to segment and get the location of S1/ S2 and use this model.**

