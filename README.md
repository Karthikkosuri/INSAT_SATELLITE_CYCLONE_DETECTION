# INSAT_SATELLITE_CYCLONE_DETECTION

## 🌀 Project Description
This project presents an automated deep learning system for estimating tropical cyclone intensity from infrared satellite images captured by the Indian National Satellite (INSAT) system. Rather than relying on time-consuming manual interpretation of satellite data, this approach directly predicts cyclone intensity as a continuous numerical value in knots — framing it as a regression problem to enable faster and more reliable forecasting.
The preprocessed satellite images are passed through three deep learning architectures to predict cyclone intensity:

* CNN (Convolutional Neural Network): A custom-built baseline architecture trained from scratch using convolutional and pooling layers to extract spatial features, achieving a validation MAE of 0.0402 and RMSE of 0.1621.
* Xception: A deep transfer learning model pre-trained on ImageNet with depthwise separable convolutions, offering improved feature abstraction with a validation MAE of 0.0341 and RMSE of 0.1514.
* MobileNetV2: A lightweight, efficient transfer learning architecture using inverted residual blocks, achieving the best performance with a validation MAE of 0.0303 and RMSE of 0.1465 — making it ideal for real-time deployment.
## 🏗️ Model Architecture & Description

All three models were configured as regression networks — predicting continuous cyclone
intensity values (in knots) rather than discrete categories. Each model was compiled with
the Adam optimizer, Mean Absolute Error (MAE) as the loss function, and Root Mean Squared
Error (RMSE) as the evaluation metric, trained for 50 epochs with a batch size of 32.

---

### 🔷 1. CNN — Custom Convolutional Neural Network

A baseline architecture built from scratch to establish a performance benchmark.

* Input: 224×224×3 resized infrared satellite images
* Conv Block 1: Conv2D (32 filters, 3×3) → Batch Normalization → MaxPooling2D → Dropout
* Conv Block 2: Conv2D (64 filters, 3×3) → Batch Normalization → MaxPooling2D → Dropout
* Conv Block 3: Conv2D (128 filters, 3×3) → Batch Normalization → MaxPooling2D → Dropout
* Head: Flatten → Dense (128, ReLU) → Dense (1, output)
* Training: 50 epochs, EarlyStopping applied on validation loss

---

### 🔶 2. Xception — Extreme Inception (Transfer Learning)

A high-performance architecture leveraging depthwise separable convolutions
pre-trained on ImageNet.

* Base: Xception (include_top=False, weights='imagenet', layers frozen)
* Input: 224×224×3 infrared satellite images
* Pooling: GlobalAveragePooling2D
* Head: Dense (128, ReLU) → Dense (1, output)
* Strategy: Feature extraction — base weights frozen, only custom head trained

---

### 🟢 3. MobileNetV2 — Lightweight Transfer Learning (Best Model ✅)

An efficient architecture using inverted residual blocks and depthwise separable
convolutions, optimized for performance with minimal computational cost.

* Base: MobileNetV2 (include_top=False, weights='imagenet', layers frozen)
* Input: 224×224×3 infrared satellite images
* Pooling: GlobalAveragePooling2D
* Head: Dense (128, ReLU) → Dense (1, output)
* Strategy: Feature extraction — converges faster due to lightweight design

---

### 📊 Performance Comparison

| Model       | Validation MAE | Validation RMSE | Approach          |
|-------------|---------------|-----------------|-------------------|
| CNN         | 0.0402        | 0.1621          | From scratch      |
| Xception    | 0.0341        | 0.1514          | Transfer learning |
| MobileNetV2 | 0.0303        | 0.1465 ✅       | Transfer learning |


## 📂 Dataset

[Download the dataset used in this experiment from here !](https://www.kaggle.com/datasets/sshubam/insat3d-infrared-raw-cyclone-images-20132021)
