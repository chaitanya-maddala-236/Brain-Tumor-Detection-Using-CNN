# Brain Tumor Detection System

A deep learning-based web application for classifying brain MRI images into four categories: **No Tumor**, **Meningioma**, **Glioma**, and **Pituitary Tumor**.

## Overview

This project leverages transfer learning with the VGG16 pre-trained model to accurately detect and classify brain tumors from MRI scans. The system achieved **95% accuracy** on the test dataset and provides a user-friendly web interface built with Flask for real-time predictions.

## Features

- **Multi-class Classification**: Classifies MRI images into four distinct categories
- **Transfer Learning**: Uses VGG16 pre-trained model for efficient feature extraction
- **Web Interface**: Simple Flask-based interface for uploading and analyzing MRI images
- **Real-time Predictions**: Instant classification results with confidence scores
- **Visual Feedback**: Displays uploaded images alongside prediction results

## Project Workflow

### 1. Data Loading and Preprocessing

- **Dataset Structure**: Separate training and testing sets organized into four folders representing each tumor category
- **Data Augmentation**: Applied rotation, contrast enhancement, and other transformations to prevent overfitting
- **Label Encoding**: Converted string labels (tumor types) into integer encodings for model training
- **Normalization**: Scaled pixel values to the range [0, 1] for optimal model performance
- **Batch Generation**: Created data batches to efficiently feed the model during training

### 2. Model Architecture

**Transfer Learning with VGG16**:
- Base model: Pre-trained VGG16 (trained on ImageNet)
- Input shape: 128×128×3 (RGB images)
- Top layers excluded to allow custom classification head
- Last few VGG16 layers unfrozen for fine-tuning on medical imagery

**Custom Layers Added**:
- Input layer (128×128×3)
- VGG16 base model (partially frozen)
- Flatten layer
- Dropout layers (for regularization)
- Dense output layer with softmax activation (4 classes)

**Model Compilation**:
- Optimizer: Adam
- Loss function: Categorical cross-entropy
- Metrics: Accuracy

### 3. Model Training

- Trained for 5 epochs using augmented training data
- Utilized data generators to handle large datasets efficiently
- Fine-tuned the last layers of VGG16 for domain-specific learning

### 4. Model Evaluation

The model's performance was assessed using multiple metrics:

- **Accuracy**: 95% overall accuracy achieved
- **Accuracy & Loss Plots**: Visualized training progress over epochs
- **Classification Report**: Detailed precision, recall, F1-score, and support for each class
- **Confusion Matrix**: Analyzed prediction patterns and misclassifications
- **ROC Curves**: Evaluated model performance across different threshold settings for each tumor type

## Technology Stack

- **Deep Learning**: TensorFlow/Keras
- **Web Framework**: Flask
- **Frontend**: HTML, CSS, Bootstrap
- **Image Processing**: Pillow, NumPy
- **Model**: VGG16 (Transfer Learning)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd brain-tumor-detection
```

2. Install required dependencies:
```bash
pip install -r requirements.txt
```

3. Ensure the trained model is placed in the `models/` directory:
```
models/model.h5
```

## Usage

1. Start the Flask application:
```bash
python app.py
```

2. Open your browser and navigate to:
```
http://127.0.0.1:5000/
```

3. Upload an MRI image through the web interface

4. View the classification result and confidence score

## Project Structure

```
brain-tumor-detection/
│
├── app.py                 # Flask application
├── requirements.txt       # Python dependencies
├── README.md             # Project documentation
│
├── models/
│   └── model.h5          # Trained model
│
├── templates/
│   └── index.html        # Web interface
│
└── uploads/              # Temporary storage for uploaded images
```

## Model Classes

The system classifies MRI images into four categories:

1. **No Tumor**: Healthy brain scans
2. **Pituitary Tumor**: Tumors in the pituitary gland
3. **Glioma**: Tumors that arise from glial cells
4. **Meningioma**: Tumors in the meninges (brain membranes)

## Results

- **Overall Accuracy**: 95%
- **Evaluation Metrics**: Comprehensive assessment using precision, recall, F1-score, and confusion matrix
- **Model Performance**: Strong classification across all four categories with minimal misclassifications

## Future Enhancements

- Implement real-time batch processing for multiple images
- Add support for additional tumor types
- Integrate explainability features (e.g., Grad-CAM) to visualize model decisions
- Deploy to cloud platforms for wider accessibility
- Implement user authentication and medical record management

## Disclaimer

This system is designed for educational and research purposes only. It should not be used as a substitute for professional medical diagnosis. Always consult qualified healthcare professionals for medical decisions.

## License

This project is open-source and available under the MIT License.

## Acknowledgments

- VGG16 model pre-trained on ImageNet
- MRI dataset contributors
- TensorFlow and Keras teams for deep learning frameworks
