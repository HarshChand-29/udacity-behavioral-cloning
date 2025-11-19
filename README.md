Here is the **complete, final `README.md`** in a single block.

This version includes the **Dataset Creation Strategy** we discussed and explicitly lists the **critical SocketIO versions** (`4.6.1`) to prevent the common simulator connection error.

### Copy & Paste this into your `README.md` file:

````markdown
# Behavioral Cloning - Self-Driving Car

This project uses a Convolutional Neural Network (CNN) to drive a car autonomously in a simulator. The model was trained using data collected from driving the car manually in the Udacity Self-Driving Car Simulator.

## Project Files
* **`model.h5`**: The saved model containing the trained weights.
* **`drive.py`**: The script to interface with the simulator, sending steering angles and throttle commands in real-time.
* **`trainingsim.py`**: The script used to create and train the model (data loading, augmentation, and network architecture).

---

## Dataset Creation & Training Strategy

The model was trained on data collected from the Udacity Simulator. The dataset creation process involved capturing images from three dashboard cameras (Center, Left, Right) along with the vehicle's steering angle, throttle, and speed.

### 1. Data Collection Strategy
To ensure the model generalizes well and doesn't just memorize the track, I used the following strategies:

* **Center Lane Driving:** I recorded 2-3 laps of smooth driving, keeping the vehicle strictly in the center of the lane to teach the "ideal" behavior.
* **Recovery Driving:** To teach the model how to handle mistakes, I recorded instances where I intentionally drove the car to the edge of the lane (near the curb) and then sharply steered back to the center. This teaches the network: *"If you see the curb this close, steer hard away from it."*
* **Reverse Direction:** Since Track 1 is heavily biased towards left turns, I drove the track in the reverse direction to balance the dataset. This prevents the model from learning to simply "steer left" constantly.

### 2. Data Preprocessing & Augmentation
Before training, the raw data was processed to improve performance:

* **Multiple Cameras:** I utilized images from the Left and Right cameras by adding a correction factor (±0.2) to the steering angle. This triples the dataset size and helps the car center itself.
* **Cropping:** The top (sky/trees) and bottom (hood of the car) of the images were cropped out, as they contain irrelevant information that confuses the model.
* **Flipping:** To further balance the left/right turn bias, I randomly flipped images horizontally and inverted the steering angle during training.

---

## How to Run

### Dependencies
**Critical:** You must use specific versions of `socketio` and `engineio` for the simulator to connect properly.

```bash
pip install python-socketio==4.6.1
pip install python-engineio==3.13.2
pip install flask
pip install eventlet
pip install keras
pip install tensorflow
pip install numpy
pip install opencv-python
````

### Execution Steps

1.  **Download the Simulator:**
    Download the Udacity Self-Driving Car Simulator [here](https://github.com/udacity/self-driving-car-sim).

2.  **Start the Drive Script:**
    Open your terminal in the project directory and run:

    ```bash
    python drive.py model.h5
    ```

3.  **Launch the Simulator:**
    Open the simulator executable, select **"Autonomous Mode"**, and the car will start driving based on your model's predictions\!

<!-- end list -->

```
