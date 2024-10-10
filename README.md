# AI System for Autonomous Vehicle Navigation

This project focuses on building an AI system to enhance the robustness of autonomous vehicles, especially when navigating rural or unfamiliar environments. The system is designed to handle three main tasks:
1. **Detect known objects in video.**
2. **Detect novel objects in video.**
3. **Make decisions to avoid collisions on the road.**

## 1. Detect Known Objects (Task 1)

In this task, we use the pre-trained YOLOv5s model for object detection.

- **Model**: YOLOv5s is a smaller version of the YOLOv5 family, known for its speed and decent performance on real-time object detection.
- **Usage**: The model is run on each video frame to identify known objects in the environment, returning bounding boxes (coordinates of detected objects) and the confidence level of each detection.

## 2. Detect Novel Objects (Task 2)

This task involves identifying objects that are unfamiliar or new to the system.

### Approach:
- **YOLOv5 Object Detection**: Run the YOLOv5 model on each frame of the video to detect objects. Each object is associated with a bounding box and a confidence score.
  
- **Novel Object Filtering**:
  - **Confidence Threshold**: Objects with low confidence scores (confidence < 0.25) are treated as potentially novel objects.
  - **Area-Based Filtering**: Objects must also have an area within a specific range to be considered for further processing. For example, objects with areas between 2000 and 10000 pixels are retained, while objects that are too small or too large are discarded.

This helps ensure that only novel objects of a reasonable size are identified, preventing false positives from noise or irrelevant objects in the background.

## 3. Collision Avoidance (Task 3)

The third task focuses on preventing collisions by identifying potential hazards and generating alerts if a collision is imminent.

### Steps:

- **Object Detection in Video**: We continue to use the YOLOv5 model to detect objects in each frame. The bounding box of each detected object is used to determine its position relative to the vehicle.

- **Defining a Safe Boundary**: A rectangular "safe zone" is defined in front of the vehicle. This zone represents an area where no objects should be present to ensure safe navigation. The safe zone's dimensions can be adjusted based on the vehicle's size and speed.

- **Collision Detection**: For every detected object, we check if its bottom part (representing its contact point with the ground) enters the safe zone. If it does, the object is flagged as a potential collision risk.

- **Collision Warning**: If an object is found within the safe boundary, the system will display a warning message such as "Collision detected" on the video frame.

## Demo

This repository contains a demo to show how the AI system works for object detection, novel object filtering, and collision avoidance in video.


