# Lung-Nodule-Segmentation
Cancer is one of the leading causes of death around the world. Early detection is a crucial step to surviving. Commonly, radiologists detect nodules using MIPs of different thicknesses. Maximum Intensity Projections (MIP) help visualize lung features over multiple scans, hence giving a clearer picture of nodules and vessels, as nodules are isolated specs and vessels, like veins, are continuous. This is better demonstrated in the figure below:

![output](https://github.com/amalmsaleem/Lung-Nodule-Segmentation/blob/main/Images/image1.png)

In this project, a similar technique is used to detect nodules. MIPs of different thicknesses are given as inputs to a Computer Aided Detection (CAD) system. This methodology is inspired by clinical practices of radiologists

### Dataset: <br />
The dataset used here is the LIDC-IDRI dataset. It is a public dataset and contains 1018 cases, each of which includes images from a clinical thoracic CT scan and an associated XML file that records the results of a two-phase image annotation process performed by four experienced thoracic radiologists.
Link to dataset here: https://wiki.cancerimagingarchive.net/display/Public/LIDC-IDRI#:~:text=The%20Lung%20Image%20Database%20Consortium,with%20marked%2Dup%20annotated%20lesions.

## Pre-processing
The following diagram shows the workflow of preprocessing the dataset.

![output](https://github.com/amalmsaleem/Lung-Nodule-Segmentation/blob/main/Images/image2.png)

The input scan is normalized to isotropic resolution i.e. a spacing of (1x1x1)mm. Then windowed to a threshold of -1000HU and 400HU.

![output](https://github.com/amalmsaleem/Lung-Nodule-Segmentation/blob/main/Images/image3.png)

After these steps, the lungs are segmented. This is done by obtaining the binary mask of lungs, then clearing the border of the lungs. This followed by applying morphology operations like erosion, closing and filling holes to result in a clean version of the mask. These steps are shown below:

![output](https://github.com/amalmsaleem/Lung-Nodule-Segmentation/blob/main/Images/image4.png)

A critical detail of this step is to make sure all nodules in the lung are included, especially the ones at the border. Usually image processing techniques tend to ignore nodules on the border.

![output](https://github.com/amalmsaleem/Lung-Nodule-Segmentation/blob/main/Images/image5.png)

After properly segmenting the lungs, MIPs of thicknesses 5,10, 15mm were generated.

![output](https://github.com/amalmsaleem/Lung-Nodule-Segmentation/blob/main/Images/image6.PNG)


## Model
Hybrid model with 3D CNN top layer and 2D UNET at bottom

## Results
Achieved 73% recall with 2 false positives per scan
