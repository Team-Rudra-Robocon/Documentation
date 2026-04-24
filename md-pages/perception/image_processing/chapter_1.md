# Overview

<sub>**Author**
Girija Kulkarni</sub>


The ABU Robocon 2026 competition, themed "Kung Fu Quest," presents a challenging autonomous navigation and object recognition task. Robot-2 must independently identify and collect Kung Fu Scrolls (KFS) while traversing the Meihua Forest arena. This task requires sophisticated vision-based perception capabilities, as manual control or teleoperation is prohibited during autonomous operation.

A Kung Fu Scroll is a three-layer cardboard box adorned with oracle bone character stickers on five visible faces, with the bottom face remaining blank. According to the competition rulebook, these scrolls are categorized as either Real KFS or Fake KFS based on the specific oracle bone characters displayed.

## Arena Challenges

The arena environment presents several technical challenges:

- The Meihua Forest consists of twelve blocks with varying elevations (200 mm, 400 mm, and 600 mm)
- Scrolls may be positioned at different heights and orientations
- Lighting conditions vary across the arena
- Visual similarity between Real and Fake scrolls requires precise classification
- Robot-2 must operate completely autonomously without human intervention

The primary objective of image processing for the autonomous robot R2 is to detect KFS in real-time frames and accurately recognize multiple KFS in a single frame in real time.