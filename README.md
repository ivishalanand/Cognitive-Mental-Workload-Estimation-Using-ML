# An automated approach for task evaluation using EEG signals

This project is an effort to use machine learning to understand the mental workload generated on an individual while performing a task and classifying the level of cognition induced in an individual.

The goal is to use various data processing techniques and ML architectures to preserve both spacial and time information in the classification of EEG data.

For a more concise and visually pleasing presentation of this project, please see the included PDF. (BTP report.pdf)

*THE EEG DATA HAS BEEN CAPTURED @BCI-HCI LAB, COMPUTER SCIENCE & ENGINEERING DEPARTMENT, IIT KHARAGPUR, INDIA.

```bash
EMOTIVE 	    - Epoc+
SENSOR COUNT    - 14+2 references
SENSOR 		    - AF3, AF4, F3, F4, FC5, FC6, F7, F8, T7, T8, P7, P8, O1, O2
SAMPLE RATE	    - 128 Hz
```

## Introduction

Critical task and cognition-based environments, such as in military
and defense operations, aviation user-technology interaction evaluation on UI, understanding intuitiveness of a hardware model or software toolkit, etc. require
an assessment of how much a particular task is generating mental workload on a
user. This is necessary for understanding how those tasks, operations, and
activities can be improvised and made better suited for the users so that they
reduce the mental workload on the individual and the operators can use them
with ease and less difficulty.

We propose an approach
to automatically evaluate the task complexity perceived by an individual by
using electroencephalogram (EEG) data of a user during operation. 

## The Data

The data are in the form of csv files with raw waveform signals from 14 probes places around the scalp. The sampling rate is 128 hz, which allows for frequency analysis up to ~60 hz. Each of 8 subjects participated in model building using SolidWorks

Each subject
underwent 3 trials. Each trial included the following steps-
- The first 5 seconds of procedure was quite; the subject was Idle.
- At the beginning of 6th second, the subject started building the model.
- Finally, after a given time limit and 5s, idle time after the experiment indicates the
end of the trial.

The link to Level 1, Level 2, Level 3 data : [CLICK HERE](https://drive.google.com/drive/folders/1zyXO-LXN4nTjpbhXkyfS7hj_QwUn8mvL?usp=sharing)




## EEG Signal Analysis

### Artifact Removal

Most of the EEG signals recorded are contaminated by artifacts and do not represent
actual brain signals. Artifacts can be significantly larger than the EEG signal, and
from various sources like muscle contraction or electromyogram (EMG), eye
movement or electrooculogram (EOG), heart activity or electrocardiogram (ECG) and
power line noise.

. In this work, the recently developed technique
called FORCe (Fully online and automated artifact removal) for brain-computer
interfacing method has been used. Following the removal of artifacts, the data is
further processed.

### Data Segmentation

From the description of the trials, the readings corresponding to the respective mental
load of a particular task from all the subjects were divided accordingly. Three trials
were taken for each individual, for each level of mental workload and were clubbed together. Each of these readings is further divided into 1-second epochs as shown in
the figure below (see Figure ). The sampling frequency of the device used is 128 Hz,
so for an epoch of 1 second, we got 128 samples.
 #### Image

### Feature Extraction

The filtered signals obtained for each epoch are of high dimension. It is important to
reduce the complexity of such high dimension signals. We extracted the features from
the processed EEG data, which gives information about distinct components of the
EEG data. It is an important step, as its extraction is needed for understanding various
features of the EEG data by the machine learning algorithm. We extracted a total of
52 features which gives a lot of information about the type of brain waves we are
dealing with and helps machine learning algorithms to better understand the data.

### Feature Normalisation and selection
The features that are extracted are then normalized to bring them to a common range.
This optimization helps in reduction of inter-subject variability. Here, the extracted
features are mean-normalized

Overfitting and dimensionality curse can be minimized using feature selection and
optimization. Features which are strongly correlated to the target variables, which in
our case is the task type are selected for classification. Feature selection becomes
important because it not only decreases the number of features for further processing
but also increases the computation speed since the machine learning algorithm has to
deal with feature space of low dimension.
Feature Selection Method Used:
###### Tree-based feature selection (Extra Trees Classifier)
###### Extreme Gradient Boosting (XGBoost)
######  Correlation Feature Selection


## Results and Discussion

We used the three different types of feature selection techniques i.e. Trees Based
Feature Selection (Extra Trees Classifier), XGBoost Feature Selection and
Correlation-based Feature Selection. We were able to get the most important features
for each specific feature selection and feature important techniques. Based on the
results, we selected top 10 features for each selection technique. The results for each
of them are as follows:

`Top 10 most important features from different feature selection technique.`
Extra Trees| XGBoost |Correlation
--------|------|------
Wavelet Detailed |STD AR| Wavelet App. Entropy
Wavelet Detailed Energy| Wavelet Detailed STD |Hjorth_activity
Wavelet App. Entropy| Variance of V to V slope |Variance of V to V slope
Auto Regressor |Wavelet Appx. STD |Wavelet Detailed Energy
Wavelet Appx. STD| Kurtosis| Wavelet Appx. STD
Variance of Vertex to Ver slope| Hjorth_mobility |FFT Beta Max Power
Delta/ Theta| Wavelet App. Entropy |1st Difference Max
Wavelet Appx. mean| Delta/ Theta |FFT Alpha Max Power
FFT Delta Max Power| Wavelet App. Energy |Coefficient of Variation
Delta/ Alpha |Wavelet Appx. Mean| FFT Theta Max Power

Comparisons were done in the classification of the target variable using all features
and only the selected features. We found that although the selected features were
comparatively less accurate but they proved to classify the target value to a great
extent. Below is the table containing the overall accuracy of different machine
learning models when all features were used and when only a limited number of
selected features were used.tc
## Conclusion
One of the initial goals of the project was to explore the feasibility of wireless data
acquisition devices in task evaluation and MWL assessment. It is evident that that
approach used in the work can be used to understand the complexity of a task and this
information can be used by companies and industries to make their software,
hardware and UI toolkits better and more intuitive for the user.  From the results obtained it can be observed that XGBoost classifier
gives the best accuracy in comparison to other machine learning algorithms. We hope
that this study would be helpful in future to explore and devise new methods for
studying and understanding the task, their complexity and the mental workload
required in its operation, helping in improving the usage and user interface of various
software and hardware toolkits.
## Files information

```bash
Level-1 Data - Contains csv for the EEG readings of 8 subjects for task 1
Level-2 Data - Contains csv for the EEG readings of 8 subjects for task 2
Level-3 Data - Contains csv for the EEG readings of 8 subjects for task 3
BTP_Code.ipynb - Contains the project code
Normalsiedfeatures.csv - contains the data after applying Force Algorithm
features.csv - Contains the fully feature engineered dataset of the EEG signals
```
## Contribution
**Vishal Anand**- Department of Mechanical Engineering, IIT Kharagpur  
**Zaki Ahmed** - Department of Mechanical Engineering, IIT Kharagpur  
**Sr Sreeja** - Department of Computer Science and Engineering, IIT Kharagpur
