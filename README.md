### Brain Tumor Detection Project
 #### Project BackGround
Brain tumors are serious neurological conditions that require early and accurate diagnosis for effective treatment. Magnetic Resonance Imaging (MRI) is widely used for detecting brain abnormalities; however, manual interpretation of MRI scans is time-consuming and may lead to diagnostic errors due to the complexity of medical images. Traditional image processing and machine learning methods often struggle to extract meaningful features from such data.

Convolutional Neural Networks (CNNs) have demonstrated strong performance in medical image analysis by automatically learning features from raw MRI images.  

This project aims to develop an enhanced CNN-based model for automatic brain tumor detection from MRI images to improve diagnostic accuracy and support healthcare professionals in timely decision-making.

 #### Objectives:

- To design and implement a CNN model for classifying MRI images into tumor and non-tumor categories.

- To evaluate the performance of the model using accuracy, precision, recall, and F1-score.

Building a detection model using a convolutional neural network in Tensorflow & Keras.
Used a brain MRI images data founded on Kaggle. You can find it here.

 #### About the data:
The dataset contains 2 folders: yes and no which contains 253 Brain MRI Images. The folder yes contains 155 Brain MRI Images that are tumorous and the folder no contains 98 Brain MRI Images that are non-tumorous.

Getting Started
Note: sometimes viewing IPython notebooks using GitHub viewer doesn't work as expected, so you can always view them using nbviewer.

Data preprocessing ivolved:  

- resizing of images to achieve consistency in the dataset in terms of shape and size for faster model training and reduction of mismatch errors in the model.
- Intensity Normalization - since MRI images have different brightness and contrast and with variation in pixel intensity, normalization will help to scale pixel values making making model focus on tumor features, improves convergence.
- Skull stripping - Remove any irrelevant non-brain tissues like sculp , eyes,or background which will improve localization accuracy , improve false positive cases.
- Data Augmantation - since MRI data set is small and the images may vary in shape,orientation and size, augmantation will help increasing image size and create variations in existing images, this will prevent overfitting, make model more robust to rotation and scale changes.




Then data was split in the following way:

70% of the data for training.
15% of the data for validation.
15% of the data for testing.

### Data Augmentation  
Because the dataset has only 253 images, augmentation is essential to:  


- Prevent overfitting
- Artificially expand training diversity
- Improve robustness to orientation / brightness variation
Augmentation was applied only to the training set at fit time — validation and test sets are untouched.

Augmentation Pipeline  
<img width="3132" height="1003" alt="image" src="https://github.com/user-attachments/assets/5590df8e-7de2-4540-9008-8839b701f2ae" />


 #### Model Training 
Neural Network Architecture  

- CNN was the most preffered model for this project since it has sophisticated tools that are well designed for image recognition and processing tasks. CNN has a powerful framework for generative and descriptive image analysis tasks.
- Due to dataset size we only had 257 images, building a CNN model from scartch was a challenge since the model had high chances of memorizing instead of learning,
- It was therefore prefferable to use VGG16 model directly since its know to have already learned from a variety of image features.
Understanding the architecture:
Each input x (image) has a shape of (240, 240, 3) and is fed into the neural network. And, it goes through the following layers:

- VGG16 Pretrained Feature Extraction Backbone (Frozen Layers)
 - Feature Maps Generation→ AveragePooling2D (4×4)→ Flatten Layer
 - Dense Layer (64, ReLU)→ Batch Normalization→ Dropout (0.5)
 - Output Layer (Dense(2), Softmax)
 -  Brain Tumor Prediction (Tumor / No Tumor)



### Classification Report
- 4 healthy cases were being missclasified as unlhealthy which might lead to further investigations and resource wastage ; since the goal is to accurately identify tumor cases only 1 image with tumor has been misclassified   

- Model had high sensitivity and low specificity;  contributed by; dataset imbalance
<img width="1556" height="1078" alt="image" src="https://github.com/user-attachments/assets/79e43184-c05f-4f20-abfa-ae57fef084d4" />


Loss plot and and accuracy plot was as displayed.  

- From visual training curves show steady convergence with decreasing loss and increasing accuracy. Validation performance remains high throughout training, with minor fluctuations due to the small dataset size. No significant overfitting is observed, indicating good generalization of the VGG16-based model.
  
- RCO curve indicates the model records high AUC of 0.9507, with high recall and less false positives which is a key metric in medical detection
  
- There is clear probability separation


  
  ROC CURVE <img width="2082" height="730" alt="image" src="https://github.com/user-attachments/assets/b096b7aa-2da8-4272-bdab-1c5782340228" />

