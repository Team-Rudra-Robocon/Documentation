# Dataset Augmentation

<sub>**Author**
Girija Kulkarni</sub>


To create a robust training dataset suitable for varying competition conditions, we implemented a comprehensive data augmentation pipeline.

## Source Data Collection

- Oracle bone character symbols were extracted from the competition rulebook
- High-resolution images were captured of each symbol type
- Base symbol size standardized to 640 × 640 pixels
- Three categories organized: R1/REAL, R2/REAL, and R2/FAKE

## Augmentation Strategy

This augmentation pipeline performs a two-step data augmentation process for object detection training.

### Step 1: Single-Object Augmentation

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

### Step 2: Multi-Object Scene Composition

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