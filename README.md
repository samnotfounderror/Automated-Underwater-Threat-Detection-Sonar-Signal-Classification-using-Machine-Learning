# Automated Underwater Threat Detection: Sonar Signal Classification using Support Vector Machines

[![Python](https://img.shields.io/badge/Python-3.10-blue)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.3-orange)](https://scikit-learn.org/)
[![Accuracy](https://img.shields.io/badge/Accuracy-81%25-brightgreen)](https://github.com/yourusername/sonar-threat-detection-ml)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Complete-success)](https://github.com/yourusername/sonar-threat-detection-ml)

## 🎯 Project Overview

This project implements a **machine learning pipeline** to classify underwater sonar signals as either **naval mines (metal cylinders)** or **natural rocks**. The system analyzes 60 frequency-band features from acoustic backscatter data to make real-time threat detection decisions with **81%+ accuracy**.

**Real-world application**: This technology can be deployed on Autonomous Underwater Vehicles (AUVs), submarines, and naval surveillance systems to automatically identify underwater threats without human intervention.

## 📊 Dataset

| Property | Details |
|----------|---------|
| **Source** | UCI Machine Learning Repository |
| **Samples** | 208 observations (111 mines, 97 rocks) |
| **Features** | 60 numerical values (0.0-1.0 range) |
| **Labels** | 'M' (Mine) and 'R' (Rock) |
| **Data Type** | Acoustic sonar backscatter signals |

Each feature represents the **energy within a specific frequency band** of the sonar signal, integrated over a particular time period—creating a unique "acoustic fingerprint" for each object.

## 🧠 Machine Learning Approach

### Models Evaluated

| Model | Test Accuracy | Strengths |
|-------|---------------|-----------|
| **Support Vector Machine (SVM)** | **81.0%** | Best for high-dimensional feature spaces |
| Random Forest | 76.2% | Handles non-linear relationships |
| Logistic Regression | 76.2% | Fast and interpretable |

### Pipeline Architecture
Raw Sonar Data (208 × 60)
↓
Data Preprocessing
├── Train-test split (80/20 with stratification)
├── Label encoding (M→1, R→0)
└── Feature standardization (StandardScaler)
↓
Model Training (3 algorithms)
↓
Evaluation Metrics
├── Accuracy score
├── Confusion matrix
├── Precision, Recall, F1-score
└── Classification report
↓
Best Model: SVM (81.0% accuracy)
↓
Prediction API (new sonar readings)


## 🔧 Technical Implementation

### Prerequisites

```bash
Python 3.8+
pip install -r requirements.txt
```

# Clone the repository
git clone https://github.com/yourusername/sonar-threat-detection-ml.git
cd sonar-threat-detection-ml

# Install dependencies
pip install -r requirements.txt

# Run the complete pipeline
python src/train.py

# Load and preprocess data
data = pd.read_csv('sonar.all-data', header=None, names=column_names)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Standardize features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)

# Train SVM classifier
svm = SVC(kernel='rbf', random_state=42)
svm.fit(X_train_scaled, y_train)

# Predict on new sonar readings
prediction = predict_sonar(svm, scaler, new_sonar_data)
