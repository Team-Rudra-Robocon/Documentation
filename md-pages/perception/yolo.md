# YOLO Algorithm

## Overview

YOLO (You Only Look Once) is a real-time object detection algorithm renowned for its speed and accuracy. Unlike earlier detection methods, YOLO processes the entire image in a single pass, providing efficient and simultaneous object localization and classification.

## Working Principle

- **Single Pass Detection:**  
  YOLO analyzes the entire image in one go, not through sliding windows or multiple region proposals.

- **Grid Division:**  
  The image is divided into an \( S \times S \) grid (e.g., 4x4, 13x13). Each grid cell is responsible for detecting objects whose centers fall inside it.

- **Prediction Vector (Per Cell):**  
  Each cell outputs a vector containing:  
    - \( p_c \): Probability of object presence  
    - \( b_x, b_y \): Coordinates of bounding box center (relative to cell)  
    - \( w, h \): Bounding box width and height  
    - Class probabilities (e.g., dog, person, etc.)

## Multi-Object Handling

- **Anchor Boxes:**  
  If multiple objects’ centers fall in the same grid cell, YOLO uses multiple anchor boxes (extra vectors per cell), allowing localization of overlapping or nearby objects of different classes.

## Output Tensor

- Output tensor shape: \( S \times S \times (B \times (5 + C)) \), where:  
  - \( S \): number of grid divisions per side  
  - \( B \): number of anchors per cell  
  - 5 represents (\( p_c, b_x, b_y, w, h \))  
  - \( C \): number of classes

## Post-Processing

- **Non-Maximum Suppression (NMS):**  
  After predictions, NMS removes duplicate bounding boxes for the same object by:  
    - Calculating Intersection-over-Union (IoU) between boxes  
    - Retaining the box with the highest confidence if IoU exceeds the overlap threshold.

## Advantages

- **Speed:**  
  Extremely fast, capable of real-time object detection in video streams.

- **Unified Architecture:**  
  Outputs all class and location predictions in one shot.

## Applications

- Real-time detection in videos and images, robotic vision, surveillance, and autonomous vehicles.

---

### References

- [codebasics: What is YOLO algorithm? | Deep Learning Tutorial 31](https://youtu.be/ag3DLKsl2vk)
