# Overall Design Idea


<sub>**Author**
Girija Kulkarni</sub>


The vision system must fulfill the following requirements:

- Real-time object detection and classification
- Reliable communication with the robot's main controller
- Compact form factor suitable for onboard mounting
- Low power consumption to maximize operational time
- Robust performance under varying environmental conditions

## Hardware Platform Evaluation

We evaluated three potential hardware platforms for implementation:

### Platform A: NVIDIA Jetson Nano

- ARM Cortex-A57 quad-core processor with 128-core Maxwell GPU
- Suitable for running standard deep learning frameworks
- Supports both CSI camera interfaces and USB peripherals
- Requires 5V 4A power supply
- Inference speeds up to 43 FPS achievable with optimized models

### Platform B: Raspberry Pi 4

- ARM Cortex-A72 quad-core processor
- Compatible with standard Pi Camera modules and USB webcams
- Lower power requirements (5V 3A)
- Inference speeds typically range from 20-50 FPS with lightweight models
- Extensive community support and documentation

### Platform C: Integrated AI Camera Module

- Self-contained vision processing unit
- Built-in neural network acceleration hardware
- Minimal external dependencies
- Lower overall system complexity
- Direct UART/USB communication capability