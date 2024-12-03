## Index
  1. Purpose
  2. Summary
  3. Pain Point
  4. Solution

## Purpose
  - Low Cost With Distribution Computing
  - 2D to 3D Constuction With Gaussian Splatting 
  - AI Data Processing With Unify Interface

## Summary
  - 

## Pain Point
  - High Cost

## Solution
  - Gathering Available Computing Resource From Rest Mobile / Computer
  - Request

## 2D to 3D Constuction With Gaussian Splatting

### Steps in reconstructing a 3D model from 2D images [Link](https://medium.com/@popovici.cristina211/3d-reconstruction-from-2d-images-using-openmvg-and-openmvs-b23bc7adb616)

#### Index
  1. Image collection
  1. Feature extraction
  1. Feature matching
  1. Structure from Motion
  1. Dense point-cloud reconstruction
  1. Mesh Reconstruction
  1. Mesh Refinement
  1. Mesh Texturing
     
#### 1. Image collection
When reconstructing the 3D configuration of an object, it is essential to capture more than two high-quality images that overlap. Additionally, ensure that these images contain EXIF metadata, which includes crucial information such as the image’s width and height, the camera used, exposure time, and most importantly, the focal length.

#### 2. Feature extraction
Once you have collected the overlapped images, you extract features from the raw data — the images. A feature is a specific characteristic that represents relevant information. Features and their descriptors are extracted from each image. These features can include keypoints (corners, edges, and blobs), lines, or segments.

Algorithms you can use for feature detection:

SIFT (Scale-Invariant Feature Transform) — useful for the detection of the keypoints
AKAZE (Accelerated-KAZE) — alternative to SIFT when when more speed and robustness is needed
SURF (Speeded-Up Robust Features) — usually used in real-time computer vision applications

#### 3. Feature Matching
The next step is identifying corresponding features in multiple images. This step is important in determining the relative orientation of the cameras.

Not all matches are correct, so filtering the matches is an important step as well.

Algorithms you can use for feature matching:

Exhaustive Matching — involves comparing each feature in an image with all features in the other images based on a similarity measure
Nearest-Neighbor Search — the closest matching feature is found based on a similarity score

#### 4. Structure from Motion (SfM)
The objective of the SfM algorithm is to estimate the camera poses and the 3D structure of the scene, given two or more images. Once feature correspondences are established, SfM aims to estimate the camera poses for each image. Camera poses describe the position and orientation of each camera when the image was taken relative to a common coordinate system. The relative camera rotation and translation are retrieved from the essential matrix, which encodes the geometric relationship between two cameras.

Starting with an initial pair of features from two images, thus a match, we know the pixel coordinates in each image. We can calculate the ray vectors from each camera center through the pixel coordinates.

The intersection point of these two rays in 3D space will be the 3D coordinate (x, y, z) of the feature point in the real world. Bundle Adjustment can be used to optimize the 3D point positions and adjust the parameters of all cameras, minimizing reprojection errors.

The significance of sparse point clouds lies in their ability to provide an initial framework for more detailed reconstruction. They offer a quick and lightweight representation of the scene, making them ideal for real-time applications like augmented reality, autonomous navigation, and more.     
