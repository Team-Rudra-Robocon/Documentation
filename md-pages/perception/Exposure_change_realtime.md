# Real-Time Exposure Control Investigation on ReCamera 2002W Using Node-RED

## Introduction

While testing a custom YOLO model on the ReCamera 2002W, it was noticed that the model's performance changed under different lighting conditions. Dark scenes made objects harder to detect, while very bright scenes sometimes caused parts of the image to become overexposed.

To improve image consistency, an attempt was made to create a real-time exposure control system using Node-RED. The idea was to monitor the brightness of the scene and automatically adjust camera exposure before the image was processed by the YOLO model.

---

## Objective

The main goals of this work were:

- Read scene brightness in real time.
- Adjust camera exposure automatically.
- Improve image quality for YOLO inference.
- Implement the solution using Node-RED.
- Keep the existing YOLO workflow unchanged.

---

## Initial Approach

The first idea was to place a Function node between the camera node and the YOLO model node.

The planned flow was:

```text
Camera → Function Node → YOLO Model → Preview
```

The Function node would check image brightness and decide whether the exposure should be increased or decreased.

However, this approach quickly ran into problems. Function nodes can modify message data, but they cannot directly change hardware-level camera settings such as exposure.

In addition, modifying the image payload caused compatibility issues with the YOLO node because the model expects image data in a specific format.

Because of these limitations, this approach was abandoned.

---

## Attempt to Access Brightness Information

The next step was to determine whether brightness information was already available from the camera node.

A Debug node was connected directly to the camera output.

Some of the messages received were:

```text
{ code: 0, data: true, name: "enabled", type: 0 }

{ code: 0, data: "", name: "destroy", type: 0 }

{ code: 0, data: array[6], name: "create", type: 0 }

{ code: 0, data: array[2], name: "light", type: 0 }
```

Based on typical Node-RED camera workflows, an attempt was made to access brightness information using:

```javascript
msg.meta.brightness
```

This resulted in the following error:

```text
Cannot read properties of undefined (reading 'brightness')
```

This showed that the expected brightness field was not available.

At this stage, it was still unclear how brightness information was exposed by the ReCamera camera node.

---

## Python-Based Approach

A second approach involved creating a Python script to handle brightness monitoring and exposure adjustment.

The script was executed using:

```bash
python3 -u /userdata/exposure.py
```

The idea was to use the Exec node to launch the script and update exposure values dynamically.

However, another problem appeared.

Each time the Exec node received a message, a new Python process was started. Since camera frames are generated continuously, multiple copies of the script could be launched at the same time.

Potential issues included:

- Increased CPU usage
- Multiple scripts running simultaneously
- Difficulty managing exposure state
- Possible interference with the inference pipeline

Because of these limitations, this approach was also not considered suitable.

---

## Exploring ISP and Camera Controls

Several commands were investigated to determine whether exposure settings could be accessed directly.

Commands explored included:

### Checking ISP Information

```bash
cat /sys/class/isp/isp_dev/brightness
```

### Listing ISP Directories

```bash
ls /sys/class/isp/
```

### Listing Camera Controls

```bash
v4l2-ctl -d /dev/video0 --list-ctrls
```

### Attempting Exposure Changes

```bash
v4l2-ctl -d /dev/video0 --set-ctrl=exposure_absolute=<value>
```

The idea was to read brightness values, calculate a suitable exposure level, and then update the camera using V4L2 controls.

---

## Planned Workflow

The intended workflow looked like this:

```text
Inject
   ↓
Read Brightness
   ↓
Calculate Exposure
   ↓
Apply Exposure
```

This exposure-control flow would run independently from the YOLO pipeline.

The YOLO workflow remained:

```text
Camera
   ↓
YOLO (.cvimodel)
   ↓
Preview
```

---

## Problems Encountered

Several issues were encountered during development:

### Missing Brightness Data

The expected brightness value was not available in the camera node output.

Attempts to access brightness data resulted in errors because the required fields did not exist.

### Function Node Errors

The following error occurred when trying to access brightness information:

```text
Cannot read properties of undefined (reading 'brightness')
```

This prevented brightness-based exposure calculations from working.

### Python Process Management

The Python approach created difficulties because a new script instance could be launched for every incoming message.

### Unclear Camera Control Path

Although exposure-related commands were identified, it was not confirmed whether those commands actually controlled the active camera stream being used by Node-RED.

### No Visible Frame Changes

Throughout testing, no visible changes were observed in the camera feed.

Even when exposure-control ideas were implemented conceptually, the image displayed by the camera node remained unchanged.

---

## Results

The goal of creating a working real-time exposure control system was not achieved.

During testing:

- Brightness information could not be reliably obtained from the camera node.
- Function-node based exposure control failed due to missing data fields.
- The Python-based approach introduced process management issues.
- No confirmed method for controlling exposure from Node-RED was found.
- No visible change was observed in the camera output.
- The custom YOLO pipeline remained functional, but exposure control could not be integrated successfully.