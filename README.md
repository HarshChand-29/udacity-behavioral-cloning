# Behavioral Cloning (Self-Driving Car)

An autonomous driving model trained using end-to-end deep learning. The model takes raw pixels from a front-facing camera and predicts the necessary steering angle in real-time.

## Overview
* **Simulator:** Udacity Self-Driving Car Simulator
* **Framework:** Keras / TensorFlow
* **Architecture:** CNN (Convolutional Neural Network)
* **Input:** 3-Channel RGB Images
* **Output:** Steering Angle (float)

## Repository Contents
* `model.h5`: The trained model weights.
* `drive.py`: Server script to interface with the simulator via SocketIO.
* `trainingsim.py`: The training pipeline (data loading, augmentation, and model architecture).

---

## Training Approach

### 1. Data Balancing
The raw simulator data is heavily biased towards driving straight or turning left (Track 1). To prevent the model from overfitting to these biases:
* **Multiple Cameras:** Utilized Left, Center, and Right camera feeds. A correction factor (`±0.2`) was applied to side cameras to teach the car to re-center itself.
* **Flipping:** Randomly flipped images and steering angles (50% probability) to balance left vs. right turn frequency.

### 2. Preprocessing
* **Cropping:** Removed the top 70 pixels (sky/scenery) and bottom 25 pixels (car hood) to focus purely on the road lines.
* **Recovery:** specifically recorded "recovery laps" where the car starts from the shoulder and steers back to the center, ensuring the model knows how to correct errors.

---

## Quick Start

### Dependencies (Critical)
The simulator requires specific versions of SocketIO to maintain a stable connection.

```bash
pip install python-socketio==4.6.1 python-engineio==3.13.2
pip install flask eventlet keras tensorflow numpy opencv-python
