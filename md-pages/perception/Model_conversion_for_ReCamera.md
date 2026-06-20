# ReCamera 2002W Model Conversion Workflow

## Introduction

The object detection model used in this project was trained using PyTorch and saved in the `.pt` format. Although this format is suitable for training and testing on a computer, it cannot be directly deployed on the ReCamera 2002W.

The ReCamera 2002W is based on the CVITEK CV181x processor, which includes a dedicated TPU (Tensor Processing Unit) for AI inference. This TPU requires models to be in the `.cvimodel` format. Therefore, the trained model must go through a series of conversion steps before it can be deployed and executed on the device.

The complete conversion pipeline used in this project is shown below:

```text
PyTorch Model (.pt)
        ↓
ONNX Model (.onnx)
        ↓
MLIR Model (.mlir)
        ↓
Calibration Table
        ↓
INT8 CVI Model (.cvimodel)
        ↓
Deployment on ReCamera 2002W
```

---

# 1. Setting Up the Conversion Environment

## What is Used?

- Docker
- Sophgo TPU-MLIR Docker Image
- TPU-MLIR Toolkit

## Why is it Used?

The conversion tools required for ReCamera are designed to run in a Linux environment and depend on several packages and libraries. Installing these tools manually on Windows can be difficult and may result in dependency issues.

To simplify the setup process, Docker is used. Docker provides an isolated Linux environment with all the required tools for model conversion. This ensures that the conversion process remains consistent across different systems.

## Commands

### Download the Docker Image

```powershell
docker pull sophgo/tpuc_dev:v3.1
```

### Start the Docker Container

```powershell
docker run --privileged --name rtr -v ${PWD}:/workspace -it sophgo/tpuc_dev:v3.1
```

### Install TPU-MLIR

```bash
pip install tpu_mlir[all]==1.7
```

## Expected Output

```text
Successfully installed tpu_mlir
```

After launching the container:

```text
root@xxxxxxxx:/workspace#
```

This confirms that the conversion environment has been set up successfully.

---

# 2. PyTorch Model (.pt)

## Full Form

**PyTorch Model File**

## Purpose

The `.pt` file is the output generated after training the neural network. It contains the trained weights and model architecture required for inference.

Example:

```text
best.pt
```

## Why is Conversion Required?

The ReCamera TPU cannot directly execute PyTorch models. Therefore, the model must first be converted into formats that can be understood by the TPU conversion toolchain.

---

# 3. Conversion to ONNX

## Full Form

**Open Neural Network Exchange (ONNX)**

## Purpose

ONNX is an open standard format used for representing machine learning models. It allows models trained in one framework to be used in another toolchain.

## Why is it Used?

The TPU-MLIR conversion tools cannot directly process PyTorch models. ONNX serves as a bridge between the training framework and the deployment toolchain.

The conversion process is:

```text
best.pt
    ↓
best.onnx
```

## Expected Output

```text
best.onnx
```

At this stage, the model becomes framework-independent and can be processed by TPU conversion tools.

---

# 4. Conversion to MLIR

## Full Form

**Multi-Level Intermediate Representation (MLIR)**

## Purpose

MLIR is an intermediate compiler representation used to optimize machine learning models before hardware-specific compilation.

## Why is it Used?

The TPU compiler performs several optimizations on the model before generating the final deployment file. These optimizations include:

- Graph optimization
- Layer fusion
- Memory optimization
- Hardware mapping

The MLIR format acts as an intermediate step where these optimizations can be applied efficiently.

## Command

```bash
model_transform \
  --model_name yolo11n \
  --model_def yolo11n.onnx \
  --input_shapes [[1,3,640,640]] \
  --mean 0.0,0.0,0.0 \
  --scale "0.0039216,0.0039216,0.0039216" \
  --keep_aspect_ratio \
  --pixel_format rgb \
  --output_names output \
  --test_input ../image/dog.jpg \
  --test_result yolo11n_top_outputs.npz \
  --mlir yolo11n.mlir
```

## Expected Output

```text
yolo11n.mlir
```

and

```text
yolo11n_top_outputs.npz
```

The `.mlir` file is the optimized intermediate representation of the model that will be used for quantization and deployment.

---

# 5. Calibration

## What is Used?

A dataset containing representative sample images.

Example:

```text
COCO2017/
├── image1.jpg
├── image2.jpg
├── image3.jpg
...
```

## Why is it Used?

The ReCamera 2002W deployment workflow generates an INT8 model for TPU execution. Before converting the model to INT8, the compiler needs information about the range of values produced by the network.

Calibration is performed to collect this information. The resulting calibration table is then used during quantization.

This step helps maintain model accuracy after converting floating-point values to 8-bit integer values.

## Command

```bash
run_calibration \
  yolo11n.mlir \
  --dataset ../COCO2017 \
  --input_num 100 \
  -o yolo11n_calib_table
```

## Expected Output

```text
yolo11n_calib_table
```

The generated calibration table contains the quantization parameters required for INT8 model generation.

---

# 6. Generating the CVI Model

## Full Form

**CVITEK Model**

## Purpose

The `.cvimodel` file is the final deployment format supported by the TPU present in the ReCamera 2002W.

## Why is INT8 Used?

The ReCamera 2002W model conversion workflow generates an INT8 quantized model for deployment on the CV181x TPU. Therefore, INT8 quantization is a required step in the deployment process rather than an optional optimization.

The calibration table generated in the previous stage is used to perform this quantization.

The conversion process is:

```text
yolo11n.mlir
        ↓
Calibration Table
        ↓
yolo11n_int8.cvimodel
```

## Command

```bash
model_deploy \
  --mlir yolo11n.mlir \
  --quantize INT8 \
  --quant_input \
  --processor cv181x \
  --calibration_table yolo11n_calib_table \
  --test_input ../image/dog.jpg \
  --test_reference yolo11n_top_outputs.npz \
  --customization_format RGB_PACKED \
  --fuse_preprocess \
  --aligned_input \
  --model yolo11n_int8.cvimodel
```

## Expected Output

```text
yolo11n_int8.cvimodel
```

This file is the final output of the conversion pipeline and is ready to be deployed on the ReCamera device.

---

# 7. Deployment on ReCamera 2002W

## What is Used?

- ReCamera Web Interface
- Node-RED Deployment Environment

## Why is it Used?

Once the `.cvimodel` file has been generated, it must be uploaded to the ReCamera device so that it can be executed by the onboard TPU.

The model can then be integrated into a Node-RED flow for real-time object detection and inference.

##Outcomes

After deployment:
- The yolov11 model loads successfully however the user trained yolov8 model was not at all supported by ReCamera, therefore, contradictiong the official documentation. Despite the yolov8 model performed better detection rather than yolov11, the camera was unable to support the model deployment.
- Real-time inference runs on the TPU.
- Detection results are visible within the ReCamera application pipeline.

# References and Resources

1. **ReCamera Model Conversion Guide (Official Seeed Studio Documentation)**  
   https://wiki.seeedstudio.com/recamera_model_conversion/

2. **TPU-MLIR Documentation (Sophgo Official Documentation)**  
   https://tpumlir.org/

3. **ONNX Documentation**  
   https://onnx.ai/

---