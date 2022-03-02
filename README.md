# Anomaly-detection-project
Project focused on detecting anomalies in LFP cells of energy storage systems

# What is Energy Storage Systems?

<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/ess.png' width=300 align='right'/>
<br>

The rapid growth of renewable sources of energy created new challenges for energy generation. Unstable energy production is one of them. This lead to mass blackouts during summer months especially is states with high proportion of renewables energy generation, such as: California, Texas.
https://www.utilitydive.com/news/california-releases-final-root-cause-analysis-of-august-rolling-blackouts/593436/ 

Energy Storage Systems are the key element to overcome it. Energy Storage systems conserve energy when there is production suplus and provide this conserved energy during high demand hours. This provides energy networks with stability.
<img src='https://github.com/314ka4y/Anomaly-detection-project/blob/main/img/balance.png' width=600/>
<br>

# Why it is important?

The energy storage system consists of dozens of thousands of cells. Failure of one cell can lead to catastrophic results and a hazardous situation on site. On average, every month, only in Korea two sites is completely destroyed by electrical fire (2018 year)




# Overview
With the increasing number of pneumonia cases during COVID-19 are hospitals are overwhelmed with additional work. One of the main methods that are used to diagnosed pneumonia and COVID-19 is by making X rays of chrest. I was hired by a local hospital to create a model that can automatically classify person on having or not pneumonia based on their X-ray. This system should have high accuracy and high recall.

To acheive this goal, We used image recognition with DeepLearning techniques including CNN and pretrained CNN.


# Business Understanding
Our stakeholder wants to have model that can be reliable in predicting when person have pneumonia.
Additional requirement - recall at least 95%.

# Used metrics
##### Our project will answer following question:
Can we predict people with pneumonia based on their chrest X-ray?

##### Hypothesis:
H0 - Person has pneumonia

HA - There is statisticaly significant proof that the preson doesnt' have pneumonia

##### TP, TN, FP, FN definition
TP - we predicted pneumonia and it actually exist.

TN - we predicted that person didn't have pneumonia and the person actually didn't have it.

FP - We predicted pneumonia but there was no pneumonia in real life.

FN - We predicted that there is no pneumonia but it actually existed.

##### Metrics used
To compare models we will focus on 2 major metrics:

Recall(Sensitivity) - Health of people is our priority, we will be focused to minimize FN.
Accuracy - how good we can predict TP and TN. General metrics that will show model performance.


# Data Understanding
The data used for this project was sourced from a dataset:

1) Chest X-Ray Images. Year: 2018 Kermany, Daniel; Zhang, Kang; Goldbaum, Michael (2018), “Large Dataset of Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images”, Mendeley Data, V3, doi: 10.17632/rscbjbr9sj.3

https://data.mendeley.com/datasets/rscbjbr9sj/3

##### The dataset contains the following images:

Train set:

There are 1349 normal images, image name example, NORMAL-2552119-0002.jpeg

There are 4489 pneumonia images, image name example, BACTERIA-4038442-0001.jpeg

Test set:

There are 234 normal images, image name example, NORMAL-8698006-0001.jpeg

There are 390 pneumonia images, image name example, VIRUS-2040583-0001.jpeg


# Modeling

This project uses image recognition with deep learning, using the following techniques:

- Fully Connected Neural Networks

- Convolutional Neural Networks

- Pretrained Convolutional Neural Networks

1. The modeling began with a baseline Fully Connected Neural Networks. We face overfitting using this method 
2. In attemps to increase our accuracy score, we different regularization tactics 
3. We increased image resolution to overcome overfitting.
4. We used  augmentation to increase our accuracy. 
5. We used pretraince CNN models with augmentation, using ImageDataGenerator and tuning shear_range, zoom_range, and horizontal_flip. This model resulted in the hgihest accuracy, lowest loss
6. Finally we tuned decision boundaries for our classification problem and propose several methods how it can help to change model performance based on stakeholders demands. 

#  Results
Our CNN with pretrained MobileNetV2  model results are as follows:

96.41% recall

95.03% accuracy

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
│   ├── normal          # Train normal X-Ray images 
│   ├── pneumonia       # Train pneumonia X-Ray images
│   ├── test            # Test set 
│   ├── models          # Saved tensorflow model
├── img                 # Result Images in this project
├── README.md
├── Pneumonia_image_recognition.ipynb
└── Project_presentation.pdf
