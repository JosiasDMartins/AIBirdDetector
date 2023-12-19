# AI Bird Detector
This is an AI Bird Detector for multi-purpose use.

- TensorFlow with Keras API
- OpenCV
- Inception V3

## Datasets
Kaggle 525 bird species classification: 
- https://www.kaggle.com/datasets/gpiosenka/100-bird-species 

In order to reduce the number of classes for this experiment (and save some memory), this dataset is filtered to load only the bird species present in Saskatchewan.
The updated list can be found on: https://www.birdlist.org/nam/canada/saskatchewan/saskatchewan.htm

### Data Splitting
The dataset is split into three datasets:
- Training
- Test
- Validation

For the test dataset, this project combines the test and validation images provided by the original Dataset.
As a result, the test dataset has 10 images by class.
For validation, the remaining images are split into the data generator (Keras) in a 0.9/0.1 proportion (train/valid).

### Data Augmentation
The data augmentation is made by Keras Image Generator. The transformations applied are listed below:
- rotation_range=30
- width_shift_range=0.2
- height_shift_range=0.2
- shear_range=0.25
- zoom_range=0.2
- horizontal_flip=True
- fill_mode='nearest'

This generator is responsible for splitting the dataset into train/validation datasets too.

### Model
For this project, an Inception V3 with Imagenet weights is used as the base model (transfer learning) to increase the learning rate and reduce false positives.
To increase the learning and propitiate the capacity to identify the selected bird species, one Convolutional Layer with 920 features and more 5 dense layers are added.

![Model Diagram](https://github.com/JosiasDMartins/AIBirdDetector/blob/main/model_plot.png)
