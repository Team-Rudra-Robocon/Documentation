# Model Performance

<sub>**Author**
Girija Kulkarni</sub>


**For YOLOv8s model:**

- Overall mAP50 score is 96.1%
- For R1 mAP50 score is 95.9%
- For R2_REAL mAP50 score is 96.1%
- For R2_FAKE mAP50 score is 96.2%

After evaluating several object detection architectures, we selected YOLOv11-Nano as our primary model due to:

- Excellent balance between accuracy and inference speed
- Efficient architecture suitable for embedded deployment
- Lightweight design enabling CPU-based training
- Native support for real-time detection scenarios
- Proven performance in similar robotics applications

The nano variant was specifically chosen because oracle bone character symbols are relatively simple visual features that do not require larger, more complex models.