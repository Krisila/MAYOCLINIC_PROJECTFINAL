##### Krisila Hammett
# Mayo Clinic CNN 

## Introduction
The purpose of the competition was to classify the origin of patients who had an acute ischemic stroke. 
The two origins being depicted in this dataset are CE (Cardioembolic) or LAA (Large Artery Atherosclerosis). 
The task is to identify the origin of the stroke using the high resolution samples from each patient. 
This data will be displayed by patient (NOT photo), and the CE and LAA will be portions of a whole the images represent. 
For example, someone may have a result of 0.75 CE and 0.25 LAA. 
I am curious as to whether the difficulty of this project relates to the variation of each image. 
I wander if focussing on the components of the tissue, rather than the tissue itself would help to better train a model. 
I think a lot of what is preventing a successful model in this case is the shape or size of the tissue. 

## Selection of Data 
The training data is provided in the form of TIF files. 
There are over a thousand of the high resolution files available to use for the model. 
The training set includes 754 of these photos. 
Each photo has a corresponding image ID. The image ID is comprised of the patient ID and the photo number. Some patients have multiple photos, and they will all need to be accounted for when calculating the final predictions. 
### Training Data 
![image](https://user-images.githubusercontent.com/84781380/184836452-11335068-e578-4d2d-800f-6c5028f50430.png)
#### The remainder of the data can be found here -> https://www.kaggle.com/competitions/mayo-clinic-strip-ai/data
### An example of the file to be analyzed his here
![image](https://user-images.githubusercontent.com/84781380/184843399-d7fb43e7-22d5-4ab3-9a64-3c1661b1010c.png)
## Methods 
Some tools/tecniques I used for Analysis are: 
### OS, tdqm, glob
These were mainly used for organizing my data to where I could save ram, and in some cases store previous analysis for later use. 
### Pandas and Sklearn.preprossing library 
Manily used for the manipulation of the CSV data. To help get the written data where it needed to be to get the desired output. 
The label encoder was used to classify the values into binary outputs. 
### Matlablib.pyplot library and Keras.preprossing libraries
These were mainly used for manipulation of the images for use.
Subplots and tiles were also used for the manipulation of the images. 
## Results
After reformattinf the images, the images used for the models looked something like this. 
### Image Before 
![image](https://user-images.githubusercontent.com/84781380/184847161-63908e07-5e1c-4b28-9f71-cb32771eb94a.png)
### Image After 
![image](https://user-images.githubusercontent.com/84781380/184847240-2b736c45-6b42-4714-bcec-d781d04e443f.png)

The resulting image eliminated white space, and kept the shape of the images from inteferring with the model results. 
The focus of these images needed to be on the tissue components, which is why the use of tiling close ups of the images together was crucial. 
### The Model 
The model took some time. It was overtrained slighly at first multiple versions of my code were generated to determine the best model. The other versions can be found here. 
https://www.kaggle.com/code/krisilahammett/fork-of-mayo-clinic/notebook
### The Results 
The model was trained per image file not patient, so for the test data the results had to be seperated.
#### The CNN Model Summary 
![image](https://user-images.githubusercontent.com/84781380/184852089-0a906935-297d-4fa6-96c7-fe1a69202266.png)
![image](https://user-images.githubusercontent.com/84781380/184853311-ce236248-7348-4576-9fa4-7f975cb50493.png)

##### Final Accuracy: 0.979
##### Validation Accuracy: 0.6571
![image](https://user-images.githubusercontent.com/84781380/184852402-acd83e0b-b39c-4565-b4b3-1d24f5cd1c2c.png)
#### Submission File 
![image](https://user-images.githubusercontent.com/84781380/184852536-5d2c07a0-374c-4dd5-86e0-161be31ed709.png)

Overall, I do think the model was accurate. I think zooming in on the texture of the tissues while reducing the overall pixelation was the best way to run an effective model without putting too much stress on the RAM and CPU. 
## Discussion

## Summary

