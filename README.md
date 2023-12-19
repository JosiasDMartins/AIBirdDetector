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


The resulting model is presented below:
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 rescaling (Rescaling)       (None, 224, 224, 3)       0         
                                                                 
 inception_v3 (Functional)   (None, None, None, 2048)  21802784  
                                                                 
 conv2d_94 (Conv2D)          (None, 5, 5, 1024)        18875392  
                                                                 
 batch_normalization_94 (Bat  (None, 5, 5, 1024)       4096      
 chNormalization)                                                
                                                                 
 max_pooling_layer (MaxPooli  (None, 2, 2, 1024)       0         
 ng2D)                                                           
                                                                 
 flatten (Flatten)           (None, 4096)              0         
                                                                 
 dense (Dense)               (None, 3312)              13569264  
                                                                 
 leaky_re_lu_1 (LeakyReLU)   (None, 3312)              0         
                                                                 
 dropout (Dropout)           (None, 3312)              0         
                                                                 
 dense_1 (Dense)             (None, 1472)              4876736   
                                                                 
 leaky_re_lu_3 (LeakyReLU)   (None, 1472)              0         
                                                                 
 dropout_1 (Dropout)         (None, 1472)              0         
                                                                 
 dense_2 (Dense)             (None, 736)               1084128   
                                                                 
 dropout_2 (Dropout)         (None, 736)               0         
                                                                 
 dense_3 (Dense)             (None, 368)               271216    
                                                                 
 dropout_3 (Dropout)         (None, 368)               0         
                                                                 
 dense_4 (Dense)             (None, 164)               60516     
                                                                 
 dropout_4 (Dropout)         (None, 164)               0         
                                                                 
 dense_5 (Dense)             (None, 92)                15180     
                                                                 
=================================================================
Total params: 60,559,312
Trainable params: 38,754,480
Non-trainable params: 21,804,832
_________________________________________________________________

