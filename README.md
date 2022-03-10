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
Sources of data:

1) Explore data folder: 2 cluster systems with several hours of data readings.

2) Test data: 5 cluster systems consist of 1200 voltage sensors, 1200 temperature sensors, and 5 current sensors.

Test data covers the period - 8h on the 10-11 June 2021, with temperature readings every 30 seconds voltage readings every 10 seconds.

Data was artificially modified to add anomaly cells.

##### The dataset structure:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/folder_structure.png' width=600/>

Inside the data folder, we have the following structure:
"cluster_n" - number of the cluster for N cluster system

Inside each cluster folder:

- temperature 

- total state

- voltage

Folders that contain reading for each sensor based on sensor type.

Sensor readings are provided in CSV files; each file contains reading for 1 hour with different discrepancies depending on sensor type.

Overall: 
2405 sensors with > 10 000 readings for each sensor
Some data was artificially modified to increase the number of anomaly sensors.

# Modeling

We forecast prediction boundaries for sensor readings. The first is voltage sensor readings.

Voltage sensor readings plot:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/Voltage_sensors.png' width=600/>

Voltage sensors Standard deviation change over the time:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/voltage_std.png' width=600/>

### First model I used was SARIMAX. 

I predicted to define boundaries for the mean value of voltage. Resulted decision boundaries:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/SARIMA_bond.png' width=600/>

Top and bottom bondaries:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/SARIMA_bond2.png' width=600/>


##### Result: 240/240 of cells were marked positive 

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/model1_result.png' width=300/>


### Second model I used was a custom model based on data normality assumption for voltage readings distribution.

Model 2 anomalies:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/model2_anomaly.png' width=600/>

##### Result: 7/240 of cells were marked positive 

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/model2_result.png' width=300/>

###  Model I used was a custom model based on data normality assumption for voltage readings distribution and additional filter based on system's status.

Model 3 anomalies:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/model3_anomaly.png' width=600/>

##### Result: 1/240 of cells were marked positive.

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/model3_result.png' width=300/>




#  Results


Below is an image showing the result of model 3 on test data:

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/test_result.png' width=300/>


100% recall

99.5% accuracy

Below are plots of anomalies in one of the clusters(cluster 2):

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/Cluster_2_voltage_anomaly.png' width=900/>

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/Cluster_2_temperature_anomaly.png' width=900/>


# Conclusion
This type of methodology can be extremely useful in identifying anomalies in cells for further analysis. When it is used with 10 000+ cells, it allows the engineer to focus on possible problems and address them accordingly. Implementation of anomaly detection systems should allow Energy System Manufacturers to improve the safety of their systems. 



# Further Questions
See the full analysis in the [Jupyter Notebook](hhttps://github.com/314ka4y/Anomaly-detection-project/blob/main/Anomaly_detection.ipynb) or review [this presentation](https://github.com/314ka4y/Anomaly-detection-project/blob/main/Project_presentation.pdf)


# Repository Structure
```
├── data                     # contains original datasets and saved models
│   ├── explore              # small dataset for model explorations
│   ├── Test_data            # testing dataset
│   ├── report               # Doc version of report and images
│   ├── img                  # Images used in readme with keyfindings
├── README.md
├── Anomaly_detection.ipynb
└── Project_presentation.pdf
