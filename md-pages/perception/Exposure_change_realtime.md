# Real-Time Exposure Control Investigation on ReCamera 2002W Using Node-RED
While testing a custom YOLO (You Only Look Once) model on the ReCamera 2002W, it was noticed that the model performed differently under different lighting conditions. When the surroundings were dark, the camera image became difficult to see and object detection accuracy dropped. Similarly, in very bright conditions, some parts of the image became overexposed, which also affected detection.

Since YOLO depends heavily on the quality of the input image, an attempt was made to automatically adjust the camera exposure based on the brightness of the scene. The goal was to make the camera image more consistent before sending it to the YOLO model.

---

The main goals of this work were:

- Monitor scene brightness in real time.
- Adjust camera exposure automatically based on lighting conditions.
- Improve image consistency before YOLO inference.
- Integrate exposure control into the existing Node-RED workflow.
- Keep the YOLO pipeline unchanged.

---

The first idea was to place a Function node between the camera node and the YOLO model node.

The planned flow was:

```text
Camera → Function Node → YOLO Model → Preview
```

The Function node was expected to check whether the image was too dark or too bright and then adjust the exposure accordingly.

However, this approach did not work. Function nodes can only process data inside Node-RED messages and cannot directly modify hardware settings such as camera exposure.

Another issue was that modifying the image payload caused problems for the YOLO node because the model expects image data in a fixed format.

Because of these limitations, a different method had to be explored.

---

## Attempt to Access Brightness Information

The next step was to determine whether brightness information was available from the camera node.

A Debug node was connected directly to the camera output.

Some of the messages received were:

```text
{ code: 0, data: true, name: "enabled", type: 0 }

{ code: 0, data: "", name: "destroy", type: 0 }

{ code: 0, data: array[6], name: "create", type: 0 }

{ code: 0, data: array[2], name: "light", type: 0 }
```

Based on typical camera workflows, an attempt was made to access brightness information using:

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

The idea was to use an Exec node to launch the script and update exposure values dynamically.

However, another issue appeared.

Each time the Exec node received a message, a new Python process was started. Since camera frames are generated continuously, multiple copies of the script could be launched at the same time.

Potential issues included:

- Increased CPU usage
- Multiple scripts running simultaneously
- Difficulty managing exposure values
- Possible interference with the YOLO inference pipeline

Because of these limitations, this approach was not considered suitable.

---

## Exploring Camera Controls

Several commands were investigated to determine whether exposure settings could be accessed directly.

### Checking Image Signal Processor (ISP) Information

```bash
cat /sys/class/isp/isp_dev/brightness
```

### Listing ISP Directories

```bash
ls /sys/class/isp/
```

### Listing Available Camera Controls Using Video for Linux 2 (V4L2)

```bash
v4l2-ctl -d /dev/video0 --list-ctrls
```

### Attempting Exposure Changes

```bash
v4l2-ctl -d /dev/video0 --set-ctrl=exposure_absolute=<value>
```

The idea was to read brightness values, calculate a suitable exposure value, and then update the camera using Video for Linux 2 (V4L2) controls.

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

Several issues were encountered during development.

### Missing Brightness Data

The expected brightness value was not available in the camera node output.

Attempts to access brightness information resulted in errors because the required fields did not exist.

### Function Node Errors

The following error occurred while trying to read brightness information:

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

Even when exposure-control commands were generated and executed, the image displayed by the camera node remained unchanged.

---

## Results

Several approaches were explored to implement real-time exposure control on the ReCamera 2002W.

The Function node approach was unable to control camera exposure because Node-RED Function nodes only process message data and do not provide direct access to camera hardware settings.

Attempts to read brightness information from the camera output were also unsuccessful. The expected brightness field was not present in the message structure, resulting in errors such as:

```text
Cannot read properties of undefined (reading 'brightness')
```

A Python-based solution was then explored using an Exec node. However, this introduced another issue where multiple Python processes could be started as new messages entered the flow, making the approach difficult to manage.

Further investigation was carried out using Image Signal Processor (ISP) paths and Video for Linux 2 (V4L2) commands. While exposure-related commands could be identified and executed, there was no clear indication that these commands were affecting the active camera stream used by Node-RED.

After testing multiple methods, no visible change was observed in the camera feed. As a result, real-time exposure control was not successfully implemented.

The testing process helped identify several limitations of the current Node-RED workflow:

- Brightness values were not directly available from the camera node.
- Function nodes could not modify hardware-level camera settings.
- Python scripts launched through the Exec node were difficult to manage because multiple processes could be created.
- Exposure commands could be executed, but their effect on the active camera stream could not be verified.
- No measurable or visible improvement was observed in the camera feed.
