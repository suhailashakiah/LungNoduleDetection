# ML_PROJECT EVALUATION: Please open the notebook named "YOLO_FINAL.ipynb" for the neural network design, training, testing and analysis. 

# Lung-Nodule-Detection---ML_Project
Lung nodule detection using YOLO




Code Heirarchi: 
# OVERVIEW
We provide a brief overview here. Detailed analysis can be found in the jupyter notebook "YOLO_FINAL.ipynb" .
## 1. Dataset
The dataset used for this project is the LIDC-IDRI dataset. The whole dataset which is 124GB of images and annotations in the form of XML files can be obtained from the following link: 

https://wiki.cancerimagingarchive.net/display/Public/LIDC-IDRI

The dataset consists of CT scan series of varying lengths for 1018 patients with annotated nodules with diameters:

- Greater than 3 mm 
- <3 mm
- non-nodules

The first and biggest step was to organize the data. XML parsing was carried out for all the 1018 patients and a dictionary was made with SERIES ID (which identifies the slice of the CT scan series) as the key and all the nodules annotated in it as the values. 

Further, from these dictionaries, an array of pixel values was extracted from the DICOM images using the pydicom package and was stored in a separate folder after rescaling using the mean and standard deviation. Another folder contained the co-ordinates of the annotations for the corresponding images. 

A total of 3000 annotated CT images were used for training out of which 2100 were used for training and the rest for testing. 

## 2. Training 

The YOLO algorithm detects objects and predicts bounding boxes with just one pass through the image instead of multiple sliding windows. Inspired from this idea, we tried out the YOLO algorithm to detect the probabilities of the presence of a nodule in a CT scan by dividing each scan into a 16 by 16 grid. Our algorithm does not predict bounding boxes.

For more information on the YOLO algorithm, read the paper at this link: 
https://arxiv.org/abs/1506.02640


A convolutional neural network with 23 layers that was inspired from u-net and resnet was designed after multiple iterations. A batch size of 1 worked the best and training was carried out on 2100 images. 

## 3. Testing and Analysis 

An accuracy of 41% was obtained as defined by our accuracy metric. For more details please refer to the jupyter notebook. 
