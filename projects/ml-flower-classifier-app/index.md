# Machine Learning Driven Android Application for Flower Identification


![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat&logo=keras&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat&logo=opencv&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=flat&logo=googlecolab&logoColor=black)
![Android Studio](https://img.shields.io/badge/Android_Studio-3DDC84?style=flat&logo=android-studio&logoColor=white)
![TensorFlow Lite](https://img.shields.io/badge/TensorFlow_Lite-FFCA28?style=flat&logo=tensorflow&logoColor=black)



## Project Summary

This project is a machine learning-based Android application designed for real-time flower species identification from images captured using a camera or selected from the gallery. Two different datasets were used to train and evaluate the model, and a comparative analysis was performed to assess performance differences across datasets.
A deep learning model was trained using TensorFlow in Google Colab and optimized for mobile deployment using TensorFlow Lite. The trained model was integrated into an Android application to enable offline inference and fast predictions on mobile devices. The system demonstrates the full pipeline of dataset preparation, comparative model training, evaluation, optimization, and mobile deployment for practical image classification use cases.

---

## Objectives

- Design and train robust deep learning models for fine-grained flower species recognition  
- Analyze and compare model performance across two different datasets to evaluate generalization capability  
- Develop an efficient pipeline for deploying trained models on resource-constrained mobile devices  
- Enable fully offline, real-time image inference on Android without cloud dependency  
- Demonstrate practical deployment of deep learning models in real-world mobile environments  

---

## Methodology

### 1. Dataset Preparation
- Used Oxford Flower Dataset + custom dataset  
- Image preprocessing: resizing, normalization, augmentation  

### 2. Model Development
- CNN-based Sequential model using TensorFlow  
- Feature extraction and classification layers  
- Trained on multiple flower categories using Google Colab  

### 3. Training & Evaluation
- Model trained using TensorFlow/Keras  
- Evaluated using accuracy and loss metrics  
- Achieved up to **97% accuracy**  

### 4. Mobile Deployment
- Converted model to TensorFlow Lite (TFLite)  
- Integrated into Android Studio project  
- Enabled offline real-time prediction  

---

## Features

- 🌸 Real-time flower detection via camera  
- 📷 Gallery image classification  
- 📱 Offline mobile inference  
- ⚡ Lightweight optimized model  
- 🎯 High accuracy predictions  

---

## Technologies Used

- Python  
- Google Colab  
- TensorFlow / Keras  
- TensorFlow Lite  
- OpenCV  
- Android Studio  
- Machine Learning  
- Image Classification  

---

## Results

- Achieved **97% classification accuracy**  
- Successfully deployed ML model on Android device  
- Real-time prediction with low latency  
- Robust performance on unseen images  

---

## Future Work

This type of implementation can be extended beyond flower classification to other real-world offline computer vision applications where internet connectivity is limited or unavailable.

Potential extensions include:

- Offline plant disease detection systems for agriculture support  
- Wildlife species identification for field researchers and hikers  
- Medical image classification tools for low-resource healthcare environments    
- Smart mobile assistants for real-time visual understanding in remote areas  

Further improvements can also include:
- Optimizing models for even lower power consumption on mobile devices  
- Expanding to multi-task learning (classification + detection)  
- Integrating lightweight on-device learning for personalization  

---

## Conclusion

This project demonstrates the integration of deep learning and mobile development to create a practical AI-based solution for real-time flower identification. It highlights the potential of deploying machine learning models directly on mobile devices using TensorFlow Lite.

---

## Confidentiality Note

The source code, full implementation details, and certain model configuration parameters have been intentionally omitted from this repository due to academic and institutional confidentiality requirements.

Additionally, parts of the dataset and experimental configurations used during model training are not publicly shared, as they were used strictly for educational and research purposes under the University of Education, Lahore, Pakistan.

This repository provides a structured overview of the project workflow, methodology, and outcomes without exposing sensitive implementation-level details.

---

**All rights reserved © University of Education, Lahore, Pakistan.**
