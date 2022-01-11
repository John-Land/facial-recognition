# Facial Recognition. Prediction of person Identify from facial image.

Facial Recognition has been deployed in many different scenarios, most famously in mobile phones. <br>
In this project we use a subset of the "Labeled Faces in the Wild" dataset to test some models for facial recognition.

## Required Python Packages
- numpy
- pandas
- sklearn
- matplotlib
- seaborn
- tensorflow
- keras

## Data Used
The Labeled Faces in the Wild dataset can be found under below link from the University of Massachusetts. <br>
<http://vis-www.cs.umass.edu/lfw/index.html> <br>

We will use the sklearn functions specially designed to extract our sample images from the raw data. <br>
To make our test use case easier, we will only consider individuals with at least 100 images in the dataset. <br>

The dataset considered had a total of 1140 images, with dimentions (125, 94, 3). <br>
Based on the requirement of at least 100 images per person, the dataset was reduced two 5 unique labels. <br>

0: 'Colin Powell'<br>
1: 'Donald Rumsfeld'<br>
2: 'George W Bush'<br>
3: 'Gerhard Schroeder'<br>
4: 'Tony Blair'<br>

![Sample Images](training_set_sample_image_01.png)

## Training

After splitting the dataset into training set (80%) and test set (20%), 6 different deep learning models were trained in Tenserflow Keras. <br>
During each training epoch, a random 20% of the training set was held out for validation. <br>
For comparison, the accuracy on the last training epoch validation set was considered. <br>


## Evaluation and model selection with cross-validation

Below performance was achieved by the different candidate models on training set validation portion on the last training epoch.

| Model                                                                         | Validation\_Loss | Validation\_Accuracy |
| ----------------------------------------------------------------------------- | ---------------- | -------------------- |
| Model 1: Pre-Trained VGG16 + Fully Connected Layers                           | 4.650881         | 0.456522             |
| Model 2: Pre-Trained resnet50 + Fully Connected Layers                        | 26.674942        | 0.456522             |
| Model 3: Pre-Trained Xception + Fully Connected Layers                        | 26.927071        | 0.456522             |
| Model 4: Pre-Trained VGG16 + Convolutional Layers + Fully Connected Layers    | 1.026759         | 0.815217             |
| Model 5: Pre-Trained Resnet50 + Convolutional Layers + Fully Connected Layers | 1.190163         | 0.858696             |
| Model 6: Pre-Trained Xception + Convolutional Layers + Fully Connected Layers | 1.776408         | 0.576087             |

The model selected with the best Validation performance was the Model 5 (Pre-Trained Resnet50 + Convolutional Layers + Fully Connected Layers), with an validation accuracy of 85.9%. <br>

| Model                                                                         | Validation\_Loss | Validation\_Accuracy |
| ----------------------------------------------------------------------------- | ---------------- | -------------------- |
| Model 5: Pre-Trained Resnet50 + Convolutional Layers + Fully Connected Layers | 1.190163         | 0.858696             |

## Best model architecture

![Best Model (Model 5) Architecture](model_05.png)

## Results on out of sample test-set

The model selected with the best Validation performance was the Model 5 (Pre-Trained Resnet50 + Convolutional Layers + Fully Connected Layers), with an validation accuracy of 85.9%. <br>
Below out of sample performance was achieved by the best model on the test set.

| Model                                                                         | Test\_Accuracy       |
| ----------------------------------------------------------------------------- | -------------------- |
| Model 5: Pre-Trained Resnet50 + Convolutional Layers + Fully Connected Layers | 0.851                |

The model selected with the best Validation performance was the Model 5 (Pre-Trained Resnet50 + Convolutional Layers + Fully Connected Layers), with an test set accuracy of 85.1%. <br>

![Confusion Matrix Test Set](canfusion_matrix_test_set.png)

## Appendix


