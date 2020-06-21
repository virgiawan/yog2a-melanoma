[//]: # (Image References)

[accuracy]: ./images/accuracy.JPG "Accuracy"
[confusion_matrix]: ./images/confusion_matrix.JPG "Confusion Matrix"
[roc]: ./images/roc.JPG "ROC Curves"

# Skin Cancer Diagnosis App

## Developer Team:
1. [Abu Wildan Mucholladin](https://github.com/abuwildanm)
2. [Reizkian Yesaya](https://github.com/reizkian)
3. [Virgiawan Huda Akbar](https://github.com/virgiawan)
4. [Yusuf Mukti](https://github.com/yusufmukti1209)

## Introduction

## Getting Started
1. Clone this [repository](https://github.com/virgiawan/yog2a-melanoma)
```
git clone https://github.com/virgiawan/yog2a-melanoma.git
```
2. Download and unzip data from [kaggle](https://www.kaggle.com/drscarlat/melanoma) (3 GB)
```
kaggle datasets download -d drscarlat/melanoma
unzip -q melanoma.zip -d .
```
3. You're recommended to using Google Colaboratory for easy implementation, but if you're not using Google Colaboratory, please install all these libraries
```
tensorflow==2.2.0
matplotlib==3.2.1
seaborn==0.10.1
scikit-learn==0.22.2.post1
requests==2.23.0
google-cloud-storage==1.18.1
google-api-python-client==1.7.12
Werkzeug==1.0.1
Flask==1.1.2
```
4. Install [gcloud](https://cloud.google.com/sdk/install) and [gsutil](https://cloud.google.com/storage/docs/gsutil_install) tools
5. Follow the instruction from this [notebook](https://github.com/virgiawan/yog2a-melanoma/blob/master/Melanoma_(Wildan).ipynb)
6. If you want to know how we explore our model, please check all our notebooks

## Model Experiments
In experimenting with the model, we make adjustments to the following parameters:
1. Neural Network Architecture
   - ResNet50     => 50% val_accuracy
   - Vanilla CNN  => 85% val_accuracy
   - VGG16        => 90% val_accuracy
   - InceptionV3  => 92% val_accuracy
   - MobileNetV2  => 93% val_accuracy
2. Data Augmentation
   - Before data augmentation	=> overfitting
   - After data augmentation  => reduce overfitting
3. Optimizer
   - Adam     => fastest converge
   - RMSprop  => 2nd converge
   - Adagrad  => 3rd converge
   - SGD      => slowest converge
4. Learning Rate
   - 0.01   => fast but random fit
   - 0.001  => well speed & fit
   - 0.0001 => slow but well fit

## Evaluation
### Accuracy

![Accuracy][accuracy]

Before we do the improvement model, we get 85% final accuracy. It appears that the train accuracy graph always increases and the train loss graph always decreases, it means that the model learns well. However, the model is still not perfect in generalizing so that the validation graph fluctuates. After we make the improvement model, we get 94% final accuracy. As you can see that the movement of the train and validation graph are almost always same, it means the model learns and generalize well.

### Confusion Matrix

![Confusion Matrix][confusion_matrix]

- True Negative (TN)  => 29
- False Positive (FP) => 21
- False Negative (FN) => 21
- True Positive (TP)  => 29

### ROC Curves
If you want to know how to understand ROC Curves, please read: [Understanding AUC - ROC Curve](https://towardsdatascience.com/understanding-auc-roc-curve-68b2303cc9c5)

![ROC Curves][roc]

AUC Score: 0.5938

It means that our model has no discrimination capacity to distinguish between positive class and negative class. It also shows that our model is still not perfect.

### Conclusion
As you can see, our model has high accuracy but has a low AUC score. Why did it happen? According to our analysis, it happened because of the imbalanced dataset. So the data we took from Kaggle does look like it has an equal distribution, but actually the `melanoma` class data has been augmented so it can be equivalent to the `not melanoma` class data. So our model learns well to detect `not melanoma` class because it has a good variety of original data.

Another reason is also that our model tends to have the attention to color features. So if there is a lesion that has a blackish color, it can definitely be detected as `melanoma`. But if there is `melanoma` lesion that has another color, our model still fails to detect it as melanoma.

## Implementation
We made a website to implement our model. This website is deployed and hosted using Google Cloud Platform. We made this application to help users both medical and non-medical users. For medical users, this application is useful to help recognize the stage of skin cancer so that it can accelerate the process of diagnosis and treatment of diseases. For non-medical users, this is useful for detecting skin cancer early.

Please check our web app: [Melanoma Web App](http://34.101.76.215:8080/)

## References

1. [Dataset](https://www.kaggle.com/drscarlat/melanoma)
2. [Web App Source](https://github.com/virgiawan/yog2a-melanoma-web)