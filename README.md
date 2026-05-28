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

## 
<img src="https://github.com/Karthikkosuri/INSAT_SATELLITE_CYCLONE_DETECTION/blob/main/insat3d_for_reference_ds/CYCLONE_DATASET/101.jpeg?raw=true" 

## 📂 Dataset

[Download the dataset used in this experiment from here !](https://www.kaggle.com/datasets/sshubam/insat3d-infrared-raw-cyclone-images-20132021)

## 🧠 Trained Models

[Download the trained models generated in this project here !]()

## 🚀 How to Use This Repository

### 1. Clone the Repository
To get a local copy of this project up and running on your desktop, open Git Bash or
your terminal and run:

```bash
git clone https://github.com/Karthikkosuri/INSAT_SATELLITE_CYCLONE_DETECTION.git
cd INSAT_SATELLITE_CYCLONE_DETECTION
```

Install the necessary dependencies from the requirements.txt file.

```bash
pip install -r requirements.txt
```

Run the provided Jupyter notebooks to preprocess the data, train models, and make
predictions.

After downloading the repository:

```bash
INSAT_SATELLITE_CYCLONE_DETECTION
├── .git                                 # Hidden Git tracking repository folder
│
├── models                               # Saved trained model files
│   ├── CNN_model.keras                  # Trained custom CNN regression model
│   ├── Xception_model.keras             # Trained Xception transfer learning model
│   └── mobiV2_model.keras               # Trained MobileNetV2 transfer learning model (Best ✅)
│
├── Data                                 # Data management directory
│   ├── images                           # Infrared INSAT satellite images
│   └── labels.csv                       # CSV file with image paths and cyclone intensity values
│
├── CNN_model.ipynb                      # Notebook to build, train and evaluate the CNN model
├── Xception_model.ipynb                 # Notebook to build, train and evaluate the Xception model
├── MobileNetV2_model.ipynb              # Notebook to build, train and evaluate the MobileNetV2 model
├── data_preprocessing.ipynb            # Notebook for image resizing, normalization and dataset splitting
├── requirements.txt                     # Text file specifying exact development dependencies and libraries
└── README.md                            # Main markdown repository project documentation page
```

## 📊 Evaluation Results

| Model       | Validation MAE | Validation RMSE |
| :---        | :---           | :---            |
| CNN Model         | 0.0402         | 0.1621          |
| Xception Model    | 0.0341         | 0.1514          |
| MobileNetV2 Model | 0.0303 ✅      | 0.1465 ✅       |


## 🛠️ Tech Stack

| Category            | Tools / Libraries                              |
| :---                | :---                                           |
| Language            | Python 3.x                                     |
| Deep Learning       | TensorFlow, Keras                              |
| Pretrained Models   | MobileNetV2, Xception (ImageNet weights)       |
| Data Processing     | NumPy, Pandas, OpenCV                          |
| Visualization       | Matplotlib                                     |
| Development         | Jupyter Notebook                               |
| Version Control     | Git, GitHub                                    |
| Large File Storage  | Git LFS                                        |

---

## ✅ Conclusion

This project successfully demonstrates the application of deep learning models —
CNN, Xception, and MobileNetV2 — for automated cyclone intensity estimation from
infrared INSAT satellite imagery. Among the three architectures evaluated,
MobileNetV2 achieved the best performance with a validation MAE of 0.0303 and
RMSE of 0.1465, proving that lightweight pretrained models can deliver high
accuracy even on relatively small satellite datasets. The results confirm the
potential of AI-driven systems to assist meteorological departments and disaster
response teams in making faster and more reliable decisions during cyclone events.

---

## 🔮 Future Work

* Expand the dataset with a larger and more diverse collection of INSAT infrared
  satellite images to improve model generalization across varying cyclone intensities.
* Integrate multimodal meteorological inputs such as wind speed, pressure, and
  visible spectrum imagery alongside infrared data for richer feature extraction.
* Explore fine-tuning of pretrained model base layers to further reduce prediction
  error and improve performance on extreme intensity cyclones.
* Develop a real-time web or mobile dashboard for live cyclone intensity prediction
  using streaming INSAT satellite feeds.
* Investigate transformer-based architectures such as Vision Transformers (ViT) for
  capturing long-range spatial dependencies in satellite imagery.
* Extend the system to predict additional cyclone parameters such as track path,
  landfall location, and rainfall estimation.
