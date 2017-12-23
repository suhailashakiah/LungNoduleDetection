### Machine learning project for the course EL-GY 9123

# Deep Learning for Lung Nodule Detection
Lung cancer is the leading cause of cancer-related deaths in the US and worldwide. The general prognosis of lung cancer is poor because doctors tend not to find the disease until it is at an advanced stage. Five-year survival is around 54% for early stage lung cancer that is localized to the lungs, but only around 4% in advanced, inoperable lung cancer. Hence, there is a need for early detection of lung cancer nodules as early diagnosis can improve the chances of survival manifold. In this project, we use deep learning to detect lung cancer nodules. 

#### Code Hierarchi: 
1. NODULES XML PROCESSING WITHOUT REGION DUPLICATES.ipynb
2. NON NODULES XML PROCESSING WITHOUT REGION DUPLICATES.ipynb
3. NODULES DCM-XML MAPPING.ipynb
4. NON NODULES DCM-XML MAPPING
5. Creating .npy files of image pixels for training.ipynb
6. YOLO_FINAL.ipynb

Note: All codes are original. We read the paper on YOLO algorithm and coded a version appropriate for the problem at hand. The code for callback function was taken from one of the assigments in the course. 

# Overview
We provide a brief overview here. Detailed analysis can be found in the jupyter notebook "YOLO_FINAL.ipynb" .
## 1. Dataset
The LIDC-IDRI dataset was used for this project. The whole dataset which is 124 GB of images and annotations in the form of XML files can be obtained from the following link: 

https://wiki.cancerimagingarchive.net/display/Public/LIDC-IDRI

The dataset consists of CT scan series of varying lengths for 1018 patients with annotated nodules with diameters:

- Greater than 3 mm 
- <3 mm
- non-nodules

The first and biggest step was to organize the data. XML parsing was carried out for all the 1018 patients and a dictionary was made with SERIES ID (which identifies the slice of the CT scan series) as the key and all the nodules annotated in it as the values. 

Further, from these dictionaries, an array of pixel values was extracted from the DICOM images using the pydicom package and was stored in a separate folder after rescaling using the mean and standard deviation. Another folder contained the co-ordinates of the annotations for the corresponding images. 

A total of 3000 annotated CT images were used out of which 2100 were used for training and the rest for testing. 

## 2. Training 

The YOLO (You Only Look Once) algorithm detects objects and predicts bounding boxes with just one pass through the image instead of multiple sliding windows. Inspired from this idea, we tried out the YOLO algorithm to detect the probabilities of the presence of a nodule in a CT scan by dividing each scan into a 16 by 16 grid. Our algorithm does not predict bounding boxes.

For more information on the YOLO algorithm, read the paper at this link: 
https://arxiv.org/abs/1506.02640


A convolutional neural network with 18 layers that was inspired from u-net and resnet was designed after multiple iterations. A batch size of 1 worked the best and training was carried out on 2100 images. 

## 3. Testing and Analysis 

An accuracy of 65% was obtained on randomly generated testing data that the model had never seen, as defined by our accuracy metric. For more details please refer to the jupyter notebook. 

### We checked the training accuracy (not shown in the notebook) and it is very close to the testing accuracy. So we believe that the model is underfitting and are working on improving the network architecture. 

###  Work in progress: 
Change neural network architecture to increase accuracy. 
