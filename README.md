# Anomaly-detection-project
The project focused on detecting anomalies in LFP cells of energy storage systems.

# What is Energy Storage Systems?

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/ess.png' width=300 align='right'/>
<br>

The rapid growth of renewable energy sources created new challenges for energy generation. Unstable energy production is one of them. This leads to mass blackouts during the summer months, especially in states with a high proportion of renewable energy generation, such as California Texas.

https://www.utilitydive.com/news/california-releases-final-root-cause-analysis-of-august-rolling-blackouts/593436/ 

Energy Storage Systems are the key element to overcome it. Energy Storage systems conserve energy when there is a production surplus and provide this conserved energy during high-demand hours. This provides energy networks with stability.

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/balance.png' width=600/>
<br>

# Why is it important?

The energy storage system consists of dozens of thousands of cells. Failure of one cell can lead to catastrophic results and a hazardous situation on site. On average, every month, only in Korea two sites is entirely destroyed by electrical fire (2018-2019 years) 

Timeline 2018-2019:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/hazard.png' width=600/>
<br>

Source: 
Results of Investigation on EESS Fire Accident in Korea 
IEC TC 120 WG4 Convenor Misung Kim, 2018



# Business Understanding
Our stakeholder wants to have a model that can analyze the status of 10 000+ cells during commissioning and annual service works. This model should identify abnormal behavior of cells that can lead to hazards during further operations.

Abnormal behavior:

Too low/high voltage sensors readings.

Too low/high-temperature sensor readings

Current imbalance during charge/discharge.

Our model should accept raw data provided from BMS(Battery management system) systems manufactured by BMester (one of the key suppliers).

The model should be easy to use and interpret results by commissioning engineers.

# Used metrics
##### Our project will answer following question:
Can we forecast boundaries of sensors' "normal readings" limits and automatically identify cells with parameters out of these limits for further investigation.

##### Hypothesis:
H0 - Anomaly in cell

HA - There is statistically significant proof that there is no anomaly in the cell.

##### TP, TN, FP, FN definition
TP - We predicted anomaly, and it does exist

TN - We predicted that there is no anomaly and it doesn't exist

FP - We predicted an anomaly, but there was no anomaly.

FN - We predicted that there is no anomaly, but it existed.

##### Metrics used
To compare models, we will focus on two primary metrics:

Recall - Missing any anomaly case can lead to Hazard. Therefore, we are focused on finding as much as possible.

Accuracy - how well we can predict TP and TN. These are general metrics that will show model performance.

While it is impossible to say that the actual identified case will lead to Hazard, it is crucial to find and mark cells for further investigation of service engineers.

# Data Understanding
The data used for this project was sourced from a dataset:

1) Chest X-Ray Images. Year: 2018 Kermany, Daniel; Zhang, Kang; Goldbaum, Michael (2018), "Large Dataset of Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images," Mendeley Data, V3, DOI: 10.17632/rscbjbr9sj.3

https://data.mendeley.com/datasets/rscbjbr9sj/3

##### The dataset contains the following images:

The system consists of 5 clusters:

Each cluster: 

- 240 temperature sensors

- 240 voltage sensors

- 1 current senor

- data readings: every 10 sec


Overall: 
2405 sensors with > 10 000 readings for each sensor


Some data was artificially modified to increase the number of anomaly sensors.

# Modeling


#  Results


Below is an image showing the confusion matrix:
<img src='https://github.com/314ka4y/Image_classification/blob/main/img/CM_Pre-trained%20Augmented%20CNN%20224x224%20frozen%20layer%20MobileNetV2.png'/>


After changing decision boundary we managed to improve our results:

97.69% recall

95.19% accuracy

The last step was to identify boundries when we have the most model errors. We can highlight these cases and substract cases between these limits. They can be proceesed by doctors in the hospital during appointment, for better results. 
In this case our finall result will be:

99.92% recall

97.26% accuracy

6.41% Suspicious cases

Confusion matrix:

<img src='https://github.com/314ka4y/Image_classification/blob/main/img/CM_Pre-trained%20Augmented%20CNN%20200x200%20frozen%20layer%20VGG16.png'/>


# Conclusion
Due to the randomness of training results may vary when the model runs on a local machine.
This type of methodology can be extremely useful in the identification of infections and abnormalities in medical imaging (not just x-ray but MRI, CT's, etc..). The use of machine learning techniques has the potential to be extremely useful in the medical field, but it is very dependable on the quality of input training data. Machine learning algorithms trained on incorrect data might give false results in the future. 


# Further Questions
See the full analysis in the [Jupyter Notebook](https://github.com/314ka4y/Image_classification/blob/main/Pneumonia_image_recognition.ipynb) or review [this presentation](https://github.com/314ka4y/Image_classification/blob/main/Project_presentation.pdf)


# Repository Structure
```
├── data                # contains original datasets and saved models
│   ├── explore         # data for model tuning 
│   ├── raw             # actual project data
│   ├── models          # Saved tensorflow model
├── img                 # Result Images in this project
├── README.md
├── Pneumonia_image_recognition.ipynb
└── Project_presentation.pdf
