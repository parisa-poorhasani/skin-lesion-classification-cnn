# Skin Lesion Classification using CNN

A deep learning project for classifying dermoscopic skin lesion images into seven diagnostic categories using a Convolutional Neural Network (CNN) and the HAM10000 dataset.

## Overview

Skin lesion classification is an important application of computer vision and deep learning in dermatology. In this project, a custom CNN model is developed to classify dermoscopic images into seven different skin lesion categories.

The project includes:

* Exploratory Data Analysis (EDA)
* Image preprocessing and normalization
* Data augmentation
* CNN model development
* Model training and validation
* Confusion matrix analysis
* Model evaluation on the test set

> **Disclaimer:** This project is for educational and research purposes only. It is not intended for medical diagnosis or clinical decision-making.

## Dataset

This project uses the **HAM10000 (Human Against Machine with 10000 training images)** dataset, which contains 10,015 dermoscopic images of common pigmented skin lesions.

The dataset includes seven diagnostic categories:

| Code    | Diagnosis                     |
| ------- | ----------------------------- |
| `nv`    | Melanocytic nevi              |
| `mel`   | Melanoma                      |
| `bkl`   | Benign keratosis-like lesions |
| `bcc`   | Basal cell carcinoma          |
| `akiec` | Actinic keratoses             |
| `vasc`  | Vascular lesions              |
| `df`    | Dermatofibroma                |

The dataset contains both benign and malignant skin lesions.

## Exploratory Data Analysis

Several aspects of the dataset were analyzed, including:

* Patient gender distribution
* Age distribution
* Lesion type distribution
* Diagnostic acquisition methods
* Lesion localization
* Lesion distribution across genders
* Sample images from each class

## Image Preprocessing

The images were resized to:

```text
75 × 100 × 3
```

where:

* Height = 75 pixels
* Width = 100 pixels
* Channels = 3 (RGB)

Missing age values were replaced using the mean age of the dataset.

Image pixel values were standardized using the mean and standard deviation calculated from the training set.

## Data Augmentation

To improve model generalization, the following augmentation techniques were applied:

* Random rotation
* Random zoom
* Width shifting
* Height shifting

The augmentation pipeline was implemented using Keras `ImageDataGenerator`.

## CNN Architecture

A custom Convolutional Neural Network was developed with the following architecture:

```text
Input: 75 × 100 × 3

Conv2D (32 filters, 3×3, ReLU)
Conv2D (32 filters, 3×3, ReLU)
MaxPooling2D
Dropout (0.25)

Conv2D (64 filters, 3×3, ReLU)
Conv2D (64 filters, 3×3, ReLU)
MaxPooling2D
Dropout (0.40)

Flatten
Dense (128, ReLU)
Dropout (0.50)

Dense (7, Softmax)
```

The model contains approximately **3.75 million trainable parameters**.

## Training

The model was trained using:

| Parameter               | Value                    |
| ----------------------- | ------------------------ |
| Optimizer               | Adam                     |
| Initial Learning Rate   | 0.001                    |
| Loss Function           | Categorical Crossentropy |
| Batch Size              | Project configuration    |
| Maximum Epochs          | 50                       |
| Learning Rate Scheduler | ReduceLROnPlateau        |
| Number of Classes       | 7                        |

The learning rate was automatically reduced when validation accuracy stopped improving.

## Results

The final model achieved the following results:

| Metric              |   Accuracy |
| ------------------- | ---------: |
| Validation Accuracy | **78.18%** |
| Test Accuracy       | **77.33%** |

### Training Progress

The model gradually improved during training. The validation accuracy reached approximately **78%**, while the final test accuracy was **77.33%**.

### Confusion Matrix

The confusion matrix was used to analyze the classification performance across the seven lesion categories and identify classes that were more frequently confused with each other.

![Confusion Matrix](results/confusion_matrix_test.png)

## Model Architecture

![CNN Architecture](results/cnn_architecture.png)

## Sample Images

Examples of images from the seven skin lesion categories:

![Sample Images](results/cell_type_samples_grid.png)

## Project Structure

```text
skin-lesion-classification-cnn/
│
├── notebooks/
│   └── skin_lesion_classification.ipynb
│
├── results/
│   ├── cnn_architecture.png
│   ├── cell_type_samples_grid.png
│   ├── confusion_matrix_test.png
│   └── training_history.png
│
├── models/
│   └── model.keras
│
├── requirements.txt
├── .gitignore
├── README.md
└── LICENSE
```

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/skin-lesion-classification-cnn.git
cd skin-lesion-classification-cnn
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Usage

Open the Jupyter Notebook:

```bash
jupyter notebook notebooks/skin_lesion_classification.ipynb
```

Before running the notebook, download the HAM10000 dataset and place the required files according to the dataset paths used in the notebook.

## Limitations

This project has several limitations:

* The model is trained on a specific dermoscopic image dataset and may not generalize to other datasets or real-world clinical images.
* The dataset contains class imbalance between lesion categories.
* A custom CNN was used instead of pretrained architectures such as ResNet, EfficientNet, or DenseNet.
* The model's performance should not be interpreted as clinical diagnostic accuracy.

## Future Improvements

Possible improvements include:

* Using transfer learning with pretrained CNN architectures
* Applying class weighting or other imbalance-handling techniques
* Increasing image resolution
* Using more advanced data augmentation
* Performing stratified dataset splitting
* Hyperparameter optimization
* Evaluating precision, recall, F1-score, and ROC-AUC
* Using explainable AI methods such as Grad-CAM

## Technologies

* Python
* NumPy
* Pandas
* Matplotlib
* Seaborn
* Plotly
* Scikit-learn
* TensorFlow / Keras
* Pillow
