# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Program

## Developed by

## NAME : DIVYA PRIYA S
## REG NO : 212225240037

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the Face Image
faceImage = cv2.imread('b.png')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape

#resized_faceImage.shape
faceImage.shape

# Load the Sunglass image with Alpha channel
glassPNG = cv2.imread('sun glass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")

# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[135:185,130:300]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[135:185,130:300]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

plt.figure(figsize=[20,20]);

```
## Output:

<img width="362" height="441" alt="Screenshot 2026-11-01 112815" src="https://github.com/user-attachments/assets/488e9662-f79b-4bce-a7f6-be566fb710a4" />

<img width="540" height="297" alt="Screenshot 2026-11-01 112826" src="https://github.com/user-attachments/assets/77fabe24-e1bc-467e-a84e-b7ed1d2eade8" />

<img width="1025" height="186" alt="Screenshot 2026-11-01 112838" src="https://github.com/user-attachments/assets/44761f40-bb44-4520-b38d-5676d7e22d48" />

<img width="349" height="425" alt="Screenshot 2026-11-01 112849" src="https://github.com/user-attachments/assets/8ab2480a-e63a-449c-843c-8d62c45fac8e" />

<img width="1020" height="175" alt="Screenshot 2026-11-01 112906" src="https://github.com/user-attachments/assets/a52e2ac6-a566-4055-8bc9-a288a5559dee" />

<img width="1029" height="641" alt="Screenshot 2026-11-01 112930" src="https://github.com/user-attachments/assets/3863deff-53bf-4a62-abdd-c0033addf2cc" />
