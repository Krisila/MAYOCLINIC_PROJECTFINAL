##### Krisila Hammett
# Mayo Clinic CNN 

## Introduction
The purpose of the competition was to classify the origin of patients who had an acute ischemic stroke. 
The two origins being depicted in this dataset are CE (Cardioembolic) or LAA (Large Artery Atherosclerosis). 
The task is to identify the origin of the stroke using the high resolution samples from each patient. 
This data will be displayed by patient (NOT photo), and the CE and LAA will be portions of a whole the images represent. 
For example, someone may have a result of 0.75 CE and 0.25 LAA. 
I am curious as to whether the difficulty of this project relates to the variation of each image. 
I wonder if focusing on the components of the tissue, rather than the tissue itself would help to better train a model. 
I think a lot of what is preventing a successful model in this case is the shape or size of the tissue. 

## Selection of Data 
The training data is provided in the form of TIF files. 
There are over a thousand of the high resolution files available to use for the model. 
The training set includes 754 of these photos. 
The test set ony incldudes 4 of these photos, and there is a seperate data set with unknown classifications for use. 
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
There was a storage limit for the competition. My initial submission was stopped because it utlized too much. 
### Pandas and Sklearn.preprossing library 
Manily used for the manipulation of the CSV data. To help get the written data where it needed to be to get the desired output. 
The label encoder was used to classify the values into binary outputs. 
### Matlablib.pyplot library and Keras.preprossing libraries
These were mainly used for manipulation of the images for use.
Subplots and tiles were also used for the manipulation of the images. 
## Results
After reformatting the images, the images used for the models looked something like this. 
### Image Before 
![image](https://user-images.githubusercontent.com/84781380/184847161-63908e07-5e1c-4b28-9f71-cb32771eb94a.png)
### Image After 
![image](https://user-images.githubusercontent.com/84781380/184847240-2b736c45-6b42-4714-bcec-d781d04e443f.png)

The resulting image eliminated white space and kept the shape of the images from interfering with the model results. 
The focus of these images needed to be on the tissue components, which is why the use of tiling close ups of the images together was crucial. 
### The Model 
The model took some time. It was overtrained slightly at first multiple versions of my code were generated to determine the best model. The other versions can be found here. 
https://www.kaggle.com/code/krisilahammett/fork-of-mayo-clinic/notebook
### The Data 
The model was trained per image file not patient, so for the test data the results had to be separated.
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
Overall, I think the model was trained successfully. I did many different versions of my code to try and get the model validation accuracy higher, but I think the reason the accuracy was not going even higher was because there were far more CE images in the dataset than there were LAA, which was difficult to train off of. I had to make sure I was getting the LAA photos in my training dataset. I originally thought shrinking the dataset would help, but that only decreased the number of LAA I had in my training. 

The reformatting of the images was successful. The reformatting was able to capture the details of the tissues without using a large number of pixels. It also eliminated that white space that came with many of the images. Reformatting was necessary, regardless of the way it was done. The pictures were all different sizes, and some had a lot of white space. It was impossible to use just a portion of the image without losing potential data. 

Due to the data being so large, I had to split up the code into to parts. I loaded a version that created a dataset of .npy files, after splitting the important aspects of the images into their respective tiles. Then I commented out that part of the code, and I ran the code again with just the code that placed the tiles together and executed the model. I put the .npy files I had previously created with the input files. There was not a lot of test data, so I only had to do these steps for the training. The test data I was able to do in one run. 

I submitted this to the competition. 
The link to the competition is here. The data file is to big for download so the data can be viewed here as well.
https://www.kaggle.com/competitions/mayo-clinic-strip-ai/data

## Summary

I first reformatted all the TIF files. I used an algorithm I found online (Cited Below) that separated the TIF files into tiles with little white space that would provide a close up on the tissue contents. I then took the tiles and made a subplot of them. I formatted this into a plot that produced a large 504x504 numpy array for the keras model. 

The keras model appears to be still slightly overtrained. I played around with this for a while. Some of the versions I ran had little test data. Others had more, and I tried to even it out by lowering some of the parameters. 

After the model ran, I saved it, and used it on the very small test model. The patient origin came out as 100% CE, but that seems to be the more common conclusion.
![image](https://user-images.githubusercontent.com/84781380/184970106-a5fca025-678a-44e0-8b82-e8020d47970f.png)

### Bibliography 

https://www.kaggle.com/code/yusaku5739/strip-ai-processing-images-to-16x256x256-tiles/notebook

