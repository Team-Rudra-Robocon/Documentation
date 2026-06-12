# Digital Camera Working

Instead of film, a digital camera uses an **image sensor** that converts light into electrical charges.

Most cameras use:
- **CCD (Charge-Coupled Device)**
- **CMOS (Complementary Metal Oxide Semiconductor)**

Both CCD and CMOS sensors convert light into electrons.

> Note: Light travels at approximately **300,000 km/s** (186,000 miles/s).

## CCD (Charge-Coupled Device)

- Transports charge across the chip and reads it at one corner of the array.
- An ADC (Analog-to-Digital Converter) converts each pixel's charge into a digital value.

### Advantages
- High image quality
- Low noise

### Disadvantages
- High power consumption

## CMOS (Complementary Metal Oxide Semiconductor)

- Uses transistors at each pixel to amplify and move charge.

### Advantages
- Low power consumption
- Lower manufacturing cost

### Disadvantages
- Traditionally noisier images
- Lower light sensitivity

# Resolution

Resolution is the amount of detail a camera can capture and is measured in pixels.

| Resolution | Total Pixels | Description |
|------------|-------------|-------------|
| 256 × 256 | ~65,000 | Very cheap cameras |
| 640 × 480 | ~307,000 | Email and web images |
| 1216 × 912 | ~1.1 MP | Good for printing |
| 1600 × 1200 | ~2 MP | High resolution |
| 2240 × 1680 | ~4 MP | 4 MP cameras |
| 4064 × 2704 | ~11.1 MP | High-end cameras |

# Color Capture

Each photosite is color-blind and records only light intensity.

Methods:
1. Three-sensor system using a beam splitter.
2. Rotating RGB filters.
3. Bayer filter and demosaicing.

# Bayer Filter

The Bayer pattern contains:
- Red pixels
- Green pixels
- Blue pixels

There are twice as many green pixels because the human eye is most sensitive to green light.

Interpolation and demosaicing algorithms estimate the full color of each pixel.

# Controlling Light

## Aperture
Controls the size of the opening through which light enters the camera.

## Shutter Speed
Controls how long light reaches the sensor.

## Focal Length
Distance between lens and sensor, affecting magnification and zoom.

# Types of Lenses

1. Fixed Focus, Fixed Zoom
2. Optical Zoom with Autofocus
3. Digital Zoom
4. Interchangeable Lens System

# Image Formats

## TIFF (.tif, .tiff)
- Lossless
- Typically uncompressed

## JPEG (.jpg, .jpeg)
- Lossy compression
- Small file size

## GIF (.gif)
- Supports 256 colors
- Suitable for web graphics

## PNG (.png)
- Lossless
- Supports transparency

## WebP (.webp)
- Modern format developed by Google
- Smaller file sizes

# CCD vs CMOS

| Feature | CCD | CMOS |
|----------|------|-------|
| Power Consumption | High | Low |
| Image Quality | Higher | Good |
| Noise | Low | Higher |
| Cost | Higher | Lower |

# References

- https://www.explainthatstuff.com/digitalcameras.html
- https://electronics.howstuffworks.com/camera.htm
