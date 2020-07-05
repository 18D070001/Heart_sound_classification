# Heart_sound_classification

## Introduction

The 2016 PhysioNet/CinC Challenge aims to encourage the development of algorithms to classify heart sound recordings collected from a variety of clinical or nonclinical (such as in-home visits) environments. The aim is to identify, from a single short recording (10-60s) from a single precordial location, whether the subject of the recording should be referred on for an expert diagnosis.

During the cardiac cycle, the heart firstly generates the electrical activity and then the electrical activity causes atrial and ventricular contractions. This in turn forces blood between the chambers of the heart and around the body. The opening and closure of the heart valves is associated with accelerations-decelerations of blood, giving rise to vibrations of the entire cardiac structure (the heart sounds and murmurs) [1]. These vibrations are audible at the chest wall, and listening for specific heart sounds can give an indication of the health of the heart. The phonocardiogram (PCG) is the graphical representation of a heart sound recording. 

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






this repository contains a Colab notebook to classify the heart sound as normal or abnormal
