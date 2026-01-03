# Image Processing for ABU Robocon 2026

<sub>**Author**
Girija Kulkarni</sub>
 

## Overview

The ABU Robocon 2026 competition, themed "Kung Fu Quest," presents a challenging autonomous navigation and object recognition task. Robot-2 must independently identify and collect Kung Fu Scrolls (KFS) while traversing the Meihua Forest arena. This task requires sophisticated vision-based perception capabilities, as manual control or teleoperation is prohibited during autonomous operation.

A Kung Fu Scroll is a three-layer cardboard box adorned with oracle bone character stickers on five visible faces, with the bottom face remaining blank. According to the competition rulebook, these scrolls are categorized as either Real KFS or Fake KFS based on the specific oracle bone characters displayed.

### Arena Challenges

The arena environment presents several technical challenges:

- The Meihua Forest consists of twelve blocks with varying elevations (200 mm, 400 mm, and 600 mm)
- Scrolls may be positioned at different heights and orientations
- Lighting conditions vary across the arena
- Visual similarity between Real and Fake scrolls requires precise classification
- Robot-2 must operate completely autonomously without human intervention

The primary objective of image processing for the autonomous robot R2 is to detect KFS in real-time frames and accurately recognize multiple KFS in a single frame in real time.

## Dataset Development

### Image Collection

For detection and recognition purposes, the widely used YOLO algorithm and OpenCV technology are chosen. The Dataset was prepared in 3 stages.

#### Stage 1

In the first stage a total of 630 images that consisted the images of the Symbols printed on A4 sized papers with almost less than 30 cm distance between camera and the print. These images consisted of augmented versions of the images too with different grayscales and blurring effects and rotations and stretching.

The model trained on this data however was unable to detect the symbols properly due to lack of a proper facing image and the enlarged framing of the symbols.

#### Stage 2

In the second stage, the Dataset was made by augmenting photographs of REAL and FAKE symbols. Augmentations included converting images to grayscale and rotating them clockwise or counter-clockwise. Each symbol was augmented in 30 ways, resulting in a dataset of 30×30=900 images. Some of the images from the stage 1 dataset were used in the validation set of the model trained on second stage dataset.

The 15 FAKE images, 15 REAL images, and 1 image of R1 were clicked from the mobile phone and from a height of approximately two feet. This resulted in clicking the pictures of white rectangular papers, which have the FAKE and REAL symbols printed on them. These papers were kept on the floor, resulting in a very distant view of the symbol, and with a grey background behind the white paper.

The augmented images were more difficult, but the model yoloV9.pt resulted in a 90 percent mAP50 score. However, the issue faced was that the model detected the background in the frame as well. Furthermore, it was also unable to detect multiple symbols in the same frame, and the model performed poorly when it came to detecting fake R2 images as well as Fake R1.

The next step taken was to train using the yoloV11n.pt as this model version too was to be tested to be more reliable and compatible with the system. This time, the data was altered and was created from the augmentation of the symbols on a white background and a bit enlarged. These images were further augmented with the effect of a white plain background and making the perception smaller.

As a result, the model was unable to find the images with a colourful different background, and the Accuracy fell to 40 per cent.

#### Stage 3

In stage 3, the data consisted of two R1 images, one with a blue background and another with a red background, as per the actual KFS. Similarly, each REAL and FAKE symbol of R2 had 2 images per symbol, i.e. RED and BLUE background. The total number of fake images of R2 was 30, and REAL was 30. Therefore, in total, 62 images were taken. These images were augmented in two ways:

**Folder: DS_AUGMENTED_SINGLE**

It consists of 402 augmented images of R1 (201 of Blue and 201 of Red background), R2 has 26 images of each symbol with a blue background and 26 each with a red background. This brings the dataset of R2 up to 780 images. Total of 1382 images.

**DS_AUGMENTED_SCENES**

It consists of a total of 2000 images, consisting of multiple single augmented images cropped in the same frame, in order for the model to be able to recognise multiple symbols in a single frame. This was achieved using the albumentations library from ultralytics.

Therefore, the model is trained on these 2000 images. Three models were tested on this dataset: yolov8s, yolov11s and yolov11n.

### Class Structure

The model was trained to recognize three distinct classes:

- **R1_SYMBOL:** Kung Fu Scroll designated for Robot-1
- **R2_REAL:** Real Kung Fu Scroll (Robot-2 target for collection)
- **R2_FAKE:** Fake Kung Fu Scroll (Robot-2 must avoid)

This three-class structure was designed to:

- Enable Robot-2 to distinguish its target (R2_REAL) from decoys (R2_FAKE)
- Provide contextual awareness of Robot-1's scrolls in shared arena spaces
- Reduce false positive detections when multiple scroll types are visible
- Support coordination strategies between Robot-1 and Robot-2

Although Robot-2 only collects R2_REAL scrolls, detecting all three classes improves overall perception reliability and enables better decision-making in complex scenarios.

### Dataset Augmentation

To create a robust training dataset suitable for varying competition conditions, we implemented a comprehensive data augmentation pipeline.

#### Source Data Collection

- Oracle bone character symbols were extracted from the competition rulebook
- High-resolution images were captured of each symbol type
- Base symbol size standardized to 640 × 640 pixels
- Three categories organized: R1/REAL, R2/REAL, and R2/FAKE

#### Augmentation Strategy

This augmentation pipeline performs a two-step data augmentation process for object detection training.

##### Step 1: Single-Object Augmentation

**Process:**

1. Scans the source directory (DS) for images in allowed classes (R1, R2_FAKE, R2_REAL)
2. For each original image:
   - Resizes it to 640×640 pixels
   - Saves the resized original
   - Generates multiple augmented copies (200 for R1, 25 for R2 classes)

**Augmentation Techniques Applied:**

- **Geometric transformations:**
  - Rotation: ±20° (60% probability)
  - Affine: scaling 0.7-1.3×, shearing ±8° (60% probability)
  - Perspective distortion: 3-7% scale (40% probability)
- **Partial framing:**
  - Random crops at 75-100% of original size (25% probability) - simulates objects partially in frame
- **Occlusion simulation:**
  - Random black squares covering 20% (R1) or 15% (R2) of image (30% probability) - mimics objects being partially blocked
- **Camera/motion effects:**
  - Gaussian blur: 3-7 pixel radius (25% probability)
  - Motion blur: up to 7 pixels (25% probability)
- **Lighting variations:**
  - Brightness/contrast: ±20% adjustment (50% probability)
  - Hue/saturation/value shifts (30% probability)
- **Sensor noise:**
  - Gaussian noise with 0.05-0.15 standard deviation (30% probability)

##### Step 2: Multi-Object Scene Composition

1. Creates 2,000 synthetic scenes with 2-5 objects each
2. For each scene:
   - Starts with a black 640×640 canvas
   - Randomly selects objects from the augmented single-object dataset
   - Places each object at:
     - Random scale: 30-60% of original size
     - Random position on the canvas
   - Generates YOLO-format labels (class_id, center_x, center_y, width, height - all normalized)
   - Saves the composite image and corresponding label file

**Key Design Choices:**

- R1 gets 8× more augmentations (200 vs 25) because it has fewer original samples
- R1 has slightly more aggressive occlusion (20% vs 15%) to increase robustness
- Multi-object scenes train the model to detect multiple objects simultaneously and handle overlapping/crowded scenarios

This approach creates a diverse dataset that helps the model generalize to various real-world conditions like different angles, lighting, partial visibility, and multiple objects in frame.

### Model Performance

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

## Overall Design Idea

The vision system must fulfill the following requirements:

- Real-time object detection and classification
- Reliable communication with the robot's main controller
- Compact form factor suitable for onboard mounting
- Low power consumption to maximize operational time
- Robust performance under varying environmental conditions

### Hardware Platform Evaluation

We evaluated three potential hardware platforms for implementation:

#### Platform A: NVIDIA Jetson Nano

- ARM Cortex-A57 quad-core processor with 128-core Maxwell GPU
- Suitable for running standard deep learning frameworks
- Supports both CSI camera interfaces and USB peripherals
- Requires 5V 4A power supply
- Inference speeds up to 43 FPS achievable with optimized models

#### Platform B: Raspberry Pi 4

- ARM Cortex-A72 quad-core processor
- Compatible with standard Pi Camera modules and USB webcams
- Lower power requirements (5V 3A)
- Inference speeds typically range from 20-50 FPS with lightweight models
- Extensive community support and documentation

#### Platform C: Integrated AI Camera Module

- Self-contained vision processing unit
- Built-in neural network acceleration hardware
- Minimal external dependencies
- Lower overall system complexity
- Direct UART/USB communication capability

### Model Selection and Training

#### Architecture Choice

The augmentation pipeline ensured the model would be robust to:

- Varied scroll orientations as Robot-2 approaches from different angles
- Different distances between camera and scrolls
- Minor image quality variations during real-time operation

## Comparative Analysis

### Platform Comparison

| Criterion | Jetson Nano | Raspberry Pi 4 | Integrated AI Camera |
|-----------|-------------|----------------|---------------------|
| Setup Complexity | Medium | Low | High (initial) |
| Runtime Efficiency | High | Medium | Very High |
| Power Consumption | 10-20W | 8-15W | 2-5W |
| Physical Size | Medium | Medium | Very Small |
| Autonomy Level | Medium | Medium | High |
| Debugging Ease | High | High | Medium |
| Cost | Medium | Low | Medium |

## Conclusion

Through careful dataset development, model training, and hardware integration, we have created a reliable perception system that meets the stringent requirements of autonomous robotics competition. The integrated AI camera approach offers particular advantages in power efficiency, system simplicity, and competition compliance, making it the recommended solution for deployment.

Future enhancements may include multi-camera systems for 360-degree coverage, sensor fusion with other modalities (ultrasonic, LiDAR), and adaptive learning capabilities to improve performance during competition rounds.

## References

- ABU Robocon 2026 Official Rulebook
- Ultralytics YOLOv11 Documentation
- OpenCV Computer Vision Library Documentation
- Embedded Deep Learning Deployment Best Practices