# Decentralized Traffic Control System

This project, developed for SIH-2022, is an intelligent traffic management system designed to optimize traffic flow at junctions by dynamically adjusting signal timings based on real-time vehicle density. It employs a custom-trained YOLOv5 model to detect and classify vehicles from a camera feed.

The core idea is to count the number of vehicles in each lane and use this data to calculate the optimal green light duration, thereby reducing unnecessary waiting times and alleviating traffic congestion.

<p align="center">
  <a href="https://www.youtube.com/watch?v=n9tXKFQUp9s" target="_blank">
    <img src="https://img.youtube.com/vi/n9tXKFQUp9s/0.jpg" alt="Video Thumbnail" width="650" height="480">
  </a>
</p>

## How It Works

The system processes a video stream (from a file or a live camera) to analyze traffic conditions. The workflow is as follows:

1.  **Vehicle Detection**: The system captures video frames and feeds them into a custom-trained YOLOv5 model.
2.  **Vehicle Classification**: The model detects and classifies vehicles into two categories:
    *   **LMV** (Light Motor Vehicle)
    *   **HMV** (Heavy Motor Vehicle)
3.  **Density Calculation**: A weighted count is calculated to represent the traffic density. In the current implementation (`detect_new.py`), LMVs add a value of `1` to the count, while HMVs add `2`.
4.  **Output**: The total weighted count is displayed on the video feed. This count serves as the primary input for a downstream traffic light control algorithm, which would use this density value to determine the green signal duration for that lane.

## Features

*   **Real-time Detection**: Identifies vehicles in real-time from video streams.
*   **Custom Classification**: Differentiates between Light Motor Vehicles (LMV) and Heavy Motor Vehicles (HMV) for more accurate traffic density assessment.
*   **Weighted Counting**: Implements a weighted counting mechanism to better represent lane congestion.
*   **YOLOv5 Powered**: Built on the fast and accurate YOLOv5 object detection framework.

## Getting Started

Follow these steps to set up and run the project on your local machine.

### Prerequisites

Ensure you have Python 3.8+ installed. You will also need the following libraries:

*   PyTorch
*   OpenCV
*   NumPy

### Installation and Setup

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/chetankamatagi/decentralized-traffic-control-system.git
    cd decentralized-traffic-control-system
    ```

2.  **Install dependencies:**
    The project relies on the standard YOLOv5 environment. You can install the necessary packages using pip.
    ```sh
    pip install torch torchvision opencv-python numpy matplotlib
    ```

### Running Detection

The main script for vehicle counting is `detect_new.py`. It uses the custom-trained `best.pt` weights.

*   **To run on a webcam feed (source 0):**
    ```sh
    python detect_new.py --weights best.pt --source 0
    ```

*   **To run on a video file:**
    Create a folder named `videos` and place your video file (e.g., `traffic.mp4`) inside it. Then, run the following command:
    ```sh
    python detect_new.py --weights best.pt --source videos/traffic.mp4
    ```

The processed video with bounding boxes and the real-time vehicle count will be displayed on your screen.

## Model Details

*   **Architecture**: YOLOv5
*   **Weights**: The custom-trained model weights are stored in `best.pt`.
*   **Classes**: The model is trained to detect two classes: `LMV` and `HMV`.
*   **Training**: The repository includes standard YOLOv5 scripts (`train.py`, `val.py`) for re-training or fine-tuning the model on a custom dataset.
