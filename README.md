# Real-Time Gesture Detection with Transformers

This project implements a high-performance, real-time gesture detector using a **DETR (DEtection TRansformer)** model. It is designed to run from a live webcam feed, identify custom gestures, and draw bounding boxes around them.

The system is built to be easily trainable on any custom set of gestures.

## Features

* **Real-Time Inference:** Performs fast and accurate gesture detection on a live webcam stream.
* **Transformer-Based:** Uses the modern DETR architecture, which combines a CNN with a Transformer for high-precision object detection.
* **Custom Data Support:** Includes scripts and a clear workflow for collecting, annotating, and training on your own custom gestures.

## Tech Stack

* **PyTorch:** The deep learning framework used for model training and inference.
* **Transformers (DETR):** The core model architecture.
* **OpenCV:** For capturing and processing the real-time video feed.
* **Python:** The core programming language.

## Installation

Follow these steps to set up your environment and install the required dependencies.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
    cd YOUR_REPO_NAME
    ```

2.  **Create a virtual environment:**
    ```bash
    python -m venv .venv
    ```

3.  **Activate the environment:**
    * **Windows:**
        ```bash
        .\.venv\Scripts\activate
        ```
    * **macOS / Linux:**
        ```bash
        source .venv/bin/activate
        ```

4.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## How to Use

There are three main parts to using this project: collecting data, training the model, and running live inference.

### 1. Collecting Your Own Dataset (collectimages.py)

To train the model on your own gestures, you first need to collect a dataset.

1.  **Run the Collection Script:**
    The `realtimeimage.py` script is used to capture snapshots from your webcam.
    ```bash
    python realtimeimage.py
    ```
2.  **Capture Images:**
    * The script will open your webcam.
    * Position your hand to make the gesture you want to record.
    * Press the **'c' key** to capture and save an image to the `data/images` folder.
    * Capture many images for each gesture in various positions and lighting conditions (100-200 images per gesture is a good start).

3.  **Label Your Images (Annotation):**
    After collecting images, you must label them with bounding boxes.
    * A great tool for this is **LabelImg** (you can install it with `pip install labelimg`).
    * Run `labelimg` from your terminal, open your `data/images` folder, and draw a box around the gesture in each image, giving it a label (e.g., "hello", "thanks").
    * Save your annotations in the **Pascal VOC (XML)** format. This will create one `.xml` file for each `.jpg` file.

### 2. Training the Model

Once your dataset is collected and labeled:

1.  The training logic is contained within the project's scripts. You will need to configure the training script to point to your new dataset.
2.  The training process iterates through your dataset, learns the features of each gesture, and saves the best-performing model weights to the `checkpoints/` directory.


### 3. Running Real-Time Detection

Once you have a trained model, you can run the live detection.

1.  **Run the detection script:**
    ```bash
    python detrtest.py
    ```
2.  The script will open your webcam.
3.  It will load the trained model and begin drawing bounding boxes and labels in real-time for any gestures it recognizes.