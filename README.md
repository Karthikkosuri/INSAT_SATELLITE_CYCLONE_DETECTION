# INSAT_SATELLITE_CYCLONE_DETECTION

🌀 Project Description
This project presents an automated deep learning system for estimating tropical cyclone intensity from infrared satellite images captured by the Indian National Satellite (INSAT) system. Rather than relying on time-consuming manual interpretation of satellite data, this approach directly predicts cyclone intensity as a continuous numerical value in knots — framing it as a regression problem to enable faster and more reliable forecasting.
The preprocessed satellite images are passed through three deep learning architectures to predict cyclone intensity:

CNN (Convolutional Neural Network): A custom-built baseline architecture trained from scratch using convolutional and pooling layers to extract spatial features, achieving a validation MAE of 0.0402 and RMSE of 0.1621.
Xception: A deep transfer learning model pre-trained on ImageNet with depthwise separable convolutions, offering improved feature abstraction with a validation MAE of 0.0341 and RMSE of 0.1514.
MobileNetV2: A lightweight, efficient transfer learning architecture using inverted residual blocks, achieving the best performance with a validation MAE of 0.0303 and RMSE of 0.1465 — making it ideal for real-time deployment.
