## Name: D Vergin Jenifer
## Register No.: 212223240174
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
## Program:
```
V=import cv2
import numpy as np
import matplotlib.pyplot as plt


faceImage = cv2.imread("C:\\Users\\admin\\Downloads\\me.jpg")
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")

faceImage.shape

faceImage.shape

glassPNG = cv2.imread("C:\\Users\\admin\\Downloads\\sunglasses.png",-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")

glassPNG = cv2.resize(glassPNG, (190, 50))
print("image Dimension ={}".format(glassPNG.shape))

glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

faceWithGlassesNaive = faceImage.copy()

glassBGR_resized = cv2.resize(glassBGR, (210, 100))

# Shifted 3 pixels more to the right again
y1, y2 = 146, 246
x1, x2 = 116, 326 # moved right by +3
faceWithGlassesNaive[y1:y2, x1:x2] = glassBGR_resized

plt.imshow(faceWithGlassesNaive[..., ::-1])


glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))

# Normalize mask to [0, 1]
glassMask = np.uint8(glassMask / 255)

# Make a copy of the face image
faceWithGlassesArithmetic = faceImage.copy()

# Define the new region of interest (ROI) for the eyes — matches new placement
y1, y2 = 146, 246
x1, x2 = 116, 326
eyeROI = faceWithGlassesArithmetic[y1:y2, x1:x2]

# Resize both mask and glasses to match the ROI
glassBGR_resized = cv2.resize(glassBGR, (x2 - x1, y2 - y1))
glassMask_resized = cv2.resize(glassMask, (x2 - x1, y2 - y1))

# Create masked regions
maskedEye = cv2.multiply(eyeROI, (1 - glassMask_resized))
maskedGlass = cv2.multiply(glassBGR_resized, glassMask_resized)

# Combine masked eye and glasses
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Place final result back into the face image
faceWithGlassesArithmetic[y1:y2, x1:x2] = eyeRoiFinal

# Display results
plt.figure(figsize=[20,20])
plt.subplot(131); plt.imshow(maskedEye[..., ::-1]); plt.title("Masked Eye Region")
plt.subplot(132); plt.imshow(maskedGlass[..., ::-1]); plt.title("Masked Sunglass Region")
plt.subplot(133); plt.imshow(faceWithGlassesArithmetic[..., ::-1]); plt.title("Final Output")


# Place the final sunglass ROI back on the face
faceWithGlassesArithmetic[y1:y2, x1:x2] = eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20])
plt.subplot(121); plt.imshow(faceImage[:, :, ::-1]); plt.title("Original Image")
plt.subplot(122); plt.imshow(faceWithGlassesArithmetic[:, :, ::-1]); plt.title("With Sunglasses")

```
## Output:
<img width="472" height="579" alt="image" src="https://github.com/user-attachments/assets/fbbc15f9-a24b-4622-820f-1b6370dae45e" />
<img width="622" height="600" alt="image" src="https://github.com/user-attachments/assets/7249f7e4-d25f-4890-a149-6d73902f6311" />
<img width="1256" height="229" alt="image" src="https://github.com/user-attachments/assets/b2b2691b-98dd-4381-b86d-fdee25d705dd" />
<img width="490" height="562" alt="image" src="https://github.com/user-attachments/assets/46933ce9-e30b-4b1b-b6ec-67af8992ec82" />
<img width="1246" height="557" alt="image" src="https://github.com/user-attachments/assets/28df0ef4-cb00-46d7-924e-e18e5c1da8d8" />
<img width="943" height="587" alt="image" src="https://github.com/user-attachments/assets/3fe3ca8d-2054-479d-a8fa-3001e663d84a" />


