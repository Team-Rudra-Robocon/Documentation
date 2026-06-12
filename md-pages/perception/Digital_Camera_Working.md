# Digital Camera Working:

Instead of film, a digital camera has a sensor that converts light into electrical charges. Most cameras use image sensor: Charged Couple Device( CCD )

Some cameras use : Complementary Metal Oxide Semiconductor(CMOS)

Both CCD and CMOS convert light into electrons

#Light travels at a speed of around 30000 km/sec or 186000 miles/sec

## CCD:

It transports charge across chip and reads it at one corner in the array.

ADC then turns each pixel’s value into a digital value by measuring the amount of charge at each photosite and converting that measurement to binary form.

## CMOS:

These devices use several transistors at each pixel to amplify and move the charge using more traditional wires.

CMOS sensor traditionally consumes little power but CCD consumes a lot of power(100 times more than CMOS)

CCD creates high quality, low noise images, while CMOS images are more noisy.

CMOS has lower light sensitivity as many photons hit the transistor instead of photodiode.

## Resolution:

The amount of detail a camera can capture is called as Resolution and it is measured in pixels.

The more the pixels the better the image is as it captures pictures without blurry or grainy finish and has more refined details.

### Types of Resolution:

1. 256 x 256 :found on very cheap cameras, total 65000 pixels in image.
2. 640 x 480: low end on most real Cameras. Ideal resolution for email pictures or site posting/ small scale.
3. 1216 x 912 : This is a megapixel image of size ~11,09,000 total pixels. Good for printing pictures
4. 1600 x 1200: Almost 2 Million total pixels, “High Resolution”
5. 2240 x 1680 : found on 4 Megapixel cameras
6. 4064 x 2704: Top line digital cameras with 11.1 megapixels

Unfortunately each photosite is colourblind. It only keeps track of total intensity of the light that strikes it surface. For getting full colour, most use filtering to look at light in its three primary colours. Highest quality cameras use three sensors.

# A beam spitter directs the light to different sensors.

Each sensor gets an identical look at the image; but because of the filters each sensor only responds to one of the primary colours.

The advantage of this method is that the camera records each of the three colours at each pixel location.

# Another method is to rotate series of red, blue and green filters in front of single sensor.

The sensor records three separate images in rapid succession. This method also provides information on all three colours at each pixel location; but since the three images aren’t taken at precisely the same moment, both camera and target of the photo must remain stationary for all the three readings.

## Demosaicing Algorithms:

### Colour Filtering:

A more economical and practical way to record the primary colours is to permanently place a filter called a colour filter array.

By breaking up the sensor into a variety of red, blur and green pixels, it is possible to get enough information in the denereal vicinity of each sensor to make very accurate guesses about the true colour at that location.

This process of looking at the other pixels and making and educated guess is called interpolation.

The most common pattern of filters is the Bayer Filter pattern.

# Bayer Filter:

This pattern alternated a row of red and green filters with a row of blue and green filters.

The pixels are not evenly divided, there are as many as green pixels as there are red and blue combined.

This is because human ye is not equally sensitive to all three colours.

Its necessary to include more information from green pixels in order to create an image that the eye will perceive as ‘true colour’

The advantages of this method are that only one sensor is required and all the colour information (R, G and B) is recorded at the same moment.i.e. camera can be smaller and cheaper.

The raw output from a sensor with Bayer filter is a mosaic of red, green and blur pixels of different intensity.

Digital cameras use specialized demosaicing algorithms to convert this mosaic into an equally sized mosaic of true colours.

The key is that each coloured pixel can be used more than once. The true colour of a single pixel can be determined by averaging the values from closest surrounding pixels.

Digital camera has to control the amount of light that reaches the sensor.

For this is uses:

## A. Aperture:

The size of the opening in camera is its aperture. The aperture is automatic in most digital cameras, but some allow manual adjustment to gice professionals and hobbyists more control over the final image.

## B. Shutter speed:

It is the amount of time that a light can pass through the aperture. Unlike film, light sensor in Digital Camera can be reset electronically, so digital cameras have a digital shutter rather than a mechanical shutter.

#Focal length:

It is the distance between the lens and the surface of the sensor. It also determines the magnification or zoom when you look through the camera.

## Types of lenses of Digital Camera:

- Fixed Focus, Fixed Zoom lenses
- Optical-Zoom lenses with automatic focus
- Digital Zoom
- Replaceable lens system

## Types of Image Formats:

### 1. Tiff(.tif, .tiff):

Tagged Image File Format. It stores image data without losing any data. It doesn’t perform any compression of image

### 2. JPEG(.jpg, .jpeg):

Joint Photographic Experts Group. It is lossy format as data lost to reduce size of image. Good for digicam, non professional prints, Email, PPT, etc

### 3. GIF(.gif):

GIF is also know as Graphics Interchange Format files. These are used for Web Graphics. It supports 256 colours.

### 4. PNG(.png):

Portable Network Graphics files are lossless. It supports 16 million colours, made to replace GIF.

### 5. Webp:

Made by Google to replace JPEG. It uses RIFF-based container based on intra-frame cooling VP8.

## Resources:

https://www.explainthatstuff.com/digitalcameras.html

https://electronics.howstuffworks.com/camera.htm

