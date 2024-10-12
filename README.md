# UNet for Cell Nuclei Segmentation

This repository contains an implementation of the UNet architecture for segmenting cell nuclei in microscopic images. The dataset used for this implementation is taken from the Kaggle competition **2018 Data Science Bowl** — aimed at finding the nuclei in divergent images to advance medical discovery.

## Overview

UNet is a convolutional neural network specifically designed for biomedical image segmentation. Unlike typical convolutional neural networks, which focus on image classification tasks, UNet is tailored to not only determine the presence of a medical condition but also to localize the area of infection by assigning a class label to each pixel in the image.

## UNet Architecture

The UNet model comprises three main components:

1. **Contracting (Downsampling) Path**:
   - Comprises two 3x3 unpadded convolutions, each followed by a rectified linear unit (ReLU).
   - Utilizes a 2x2 max pooling operation with a stride of 2 for downsampling.
   - The number of feature channels is doubled after each downsampling operation.

2. **Bottleneck Block**:
   - Connects the contracting and expansive paths.
   - Performs two unpadded convolutions, each with 1024 filters, to prepare for the expansive path.

3. **Expansive (Upsampling) Path**:
   - Each step involves upsampling the feature map, followed by a 2x2 convolution (“up-convolution”) using transposed convolutions.
   - Concatenates with the corresponding feature map from the contracting path.
   - Applies two 3x3 convolutions, each followed by a ReLU activation.

### Skip Connections

Skip connections from the contracting path are concatenated with the corresponding feature maps in the expansive path. This helps retain higher resolution features and recover spatial information lost during downsampling.

### Final Layer

The final layer utilizes a 1x1 convolution to map each 64-component feature vector to the desired number of classes.

## Network Diagram
![image](https://github.com/user-attachments/assets/ded3eaff-cfbb-4f1b-8030-2288e03cba97)


## Results

The model effectively segments cell nuclei, as evidenced by the comparison of original masks with predicted masks from the model.
![image](https://github.com/user-attachments/assets/f599a3b1-5b4b-4702-ba68-c53e44cc8ad6)

