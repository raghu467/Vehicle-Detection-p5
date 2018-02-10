# Vehicle Detection Project
Please find the code this project in the repo with the file-name Vehicle_Detction.ipynb

Explain how (and identify where in your code) you extracted HOG features from the training images.<br>

The HOG features are extracted from the image using the hog function from skimage.feature<br>
The data set used for training the clasifier contains images of vehicle and non-vehicles of dimnetion (64*64)<br>

Data set contains the following vehicle images:<br>
Vehicle._data_set.png
Data set contains the following Vehicle Images:<br>
Non_Vehicle_images.png


The code for extracting HOG features from an image can be found in the function get_hog_features.
The figure below shows a comparison of a car and non-car images and their associated histogram of oriented gradients,
<br>
Car_hog.png
<br>
non_car_hog.png

Next, in the section titled " Extract Features for Training Datasets and Define Labels Vector, Shuffle and Split into Training and Test sets" I define parameters for HOG feature extraction and extract features for the entire Training Data-set. These feature sets  which are extracted are  then combined and a label vector is defined which tell if the feature belongs to car or non-car(1 for cars, 0 for non-cars). The features and labels are then shuffled and split into training and test sets in preparation to be fed to a linear support vector machine (SVM) classifier. Various parameter value combinations were explored for the following parameters.
orientation=11<br>
spatial_size = (64, 64)<br>
hist_bins = 16    # Number of histogram bins<br>
n_channel='ALL'   # image color-components channels in feature extraction<br>
color_space='YUV' #color space<br>
orient = 11<br>
pix_per_cell = 16<br>
cell_per_block = 2<br>



The above mentioned Hog parameters were finalized based on the SVM prediction perfomance.
HOG features,spatial intensity and channel intensity histogram features were used to train the SVM.
The code used to extract the featured from the images in the data-set can be fond in function  "extract_features" in code. 
Currently for the parameters values mentioned above the Following is the SVM prediction Accuracy.<br>
Test Accuracy of SVC =  0.985641891892<br>
The Corresponding code can be found under the section titled "SVM Training and Testing"<br>


Later after extracting the features from the data-set and training them. Sliding window search is used to search for the car images in the parts of the image extracted from the video which is meant to be processed.<br>


This funcionality is implemented using the function "slide_window" in code. This function returns all the windows feasable under the following parameters.

x_start #start of x range which windows need to be extracted <br>
x_stop  #end of x range which windows need to be extracted <br>
y_start_stop #start and stop of x range which windows need to be extracted <br>
xy_window=(64, 64) #window size<br>
xy_overlap=(0.5, 0.5) #overlaping of windows<br>

To Better improve the car detection probability the smallest possible number of windows need to be analized. To achive this we will not scan the whole image, but only areas where a new car can appear.

The following is the output of the all the windows drawn on the image which is been scaned.
Note:Different window sizes were used to be able to faithfully detect the cars which are far and near both.
The cars which are far have small size hence the window size is also reduced.

All_Windows_scan_1.png
<br>
All_Windows_scan_2.png

The car detection pipeline can be foudn in function "find_Car_in_image" in code.
several configurations of window sizes and positions, with various overlaps in the X and Y directions were explored. The following four images show the configurations of all search windows in the final implementation.

## All windows_in_images
    ystart = 380
    ystop = 650
    x_start=380
    x_stop=1250
    scale=2
    xy_window=(64*scale,64*scale)
    <br>
pipeline_2.png
## All windows_in_images

  	ystart = 380
    ystop = 470
    x_start=400
    x_stop=1000
    scale=1
    xy_window=(64*scale,64*scale)
<br>
pipeline_1.png
## heat_map
<br>
pipeline_3.png
## Filtered heat_map (Tresholded Heat-map)
<br>
pipeline_4.png
## Labled heat_map
<br>
pipeline_5.png
## Final Output with Lables over-layed
<br>
pipeline_6.png

 
<br>
 Here is the link to my final project-video.mp4 output







