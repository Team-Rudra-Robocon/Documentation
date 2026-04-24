# Dataset Development

<sub>**Author**
Girija Kulkarni</sub>



## Image Collection

For detection and recognition purposes, the widely used YOLO algorithm and OpenCV technology are chosen. The Dataset was prepared in 3 stages.

### Stage 1

In the first stage a total of 630 images that consisted the images of the Symbols printed on A4 sized papers with almost less than 30 cm distance between camera and the print. These images consisted of augmented versions of the images too with different grayscales and blurring effects and rotations and stretching.

The model trained on this data however was unable to detect the symbols properly due to lack of a proper facing image and the enlarged framing of the symbols.

### Stage 2

In the second stage, the Dataset was made by augmenting photographs of REAL and FAKE symbols. Augmentations included converting images to grayscale and rotating them clockwise or counter-clockwise. Each symbol was augmented in 30 ways, resulting in a dataset of 30×30=900 images. Some of the images from the stage 1 dataset were used in the validation set of the model trained on second stage dataset.

The 15 FAKE images, 15 REAL images, and 1 image of R1 were clicked from the mobile phone and from a height of approximately two feet. This resulted in clicking the pictures of white rectangular papers, which have the FAKE and REAL symbols printed on them. These papers were kept on the floor, resulting in a very distant view of the symbol, and with a grey background behind the white paper.

The augmented images were more difficult, but the model yoloV9.pt resulted in a 90 percent mAP50 score. However, the issue faced was that the model detected the background in the frame as well. Furthermore, it was also unable to detect multiple symbols in the same frame, and the model performed poorly when it came to detecting fake R2 images as well as Fake R1.

The next step taken was to train using the yoloV11n.pt as this model version too was to be tested to be more reliable and compatible with the system. This time, the data was altered and was created from the augmentation of the symbols on a white background and a bit enlarged. These images were further augmented with the effect of a white plain background and making the perception smaller.

As a result, the model was unable to find the images with a colourful different background, and the Accuracy fell to 40 per cent.

### Stage 3

In stage 3, the data consisted of two R1 images, one with a blue background and another with a red background, as per the actual KFS. Similarly, each REAL and FAKE symbol of R2 had 2 images per symbol, i.e. RED and BLUE background. The total number of fake images of R2 was 30, and REAL was 30. Therefore, in total, 62 images were taken. These images were augmented in two ways:

**Folder: DS_AUGMENTED_SINGLE**

It consists of 402 augmented images of R1 (201 of Blue and 201 of Red background), R2 has 26 images of each symbol with a blue background and 26 each with a red background. This brings the dataset of R2 up to 780 images. Total of 1382 images.

**DS_AUGMENTED_SCENES**

It consists of a total of 2000 images, consisting of multiple single augmented images cropped in the same frame, in order for the model to be able to recognise multiple symbols in a single frame. This was achieved using the albumentations library from ultralytics.

Therefore, the model is trained on these 2000 images. Three models were tested on this dataset: yolov8s, yolov11s and yolov11n.

## Class Structure

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
