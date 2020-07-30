# About

This repository hosts the offical implementation of VoigtNet for locating the Bragg peak position in a much fater way, compare with conventional Voigt fitting.
![VoigtNet model Architecture](img/VoigtNet.png)

# Notes

* the dataset is hard coded. you need to prepare your dataset and update the file name in the code.

# Requirement 

* PyTorch=1.5.0

# Retrain

* We provied some pre-trained model which should work well if the patch size we used make sense in your experiment. 
* if you have ground truth data, we encourage you retrain model for your use case. we tried to simplify the way to retrain the model using your own data, you only need to prepare your data based on our requirment

## Data preparation for model re-training

* Two HDF5 files are need for retrain. the first one, let's name is as frame.h5, contains your diffraction frames, this hdf5 file stores a 3D array (dataset name must be "frames"), and the first dimension is the frame ID starts with 0, i.e., the series of frames at different scanning angle. 
* The second hdf5 file stores the peak position information. In our paper, we used the peak position that we got using 2D psuedo Voigt fitting. This file stores three 1D array with each record / index represent different information of a peak. The first 1D array, must be named as "peak_fidx" represents the Id of the frame that the peak sits on; the second array, "peak_row" is the vertical distance, in pixel and can be floating point number, from the peak center to the top edge of the frame. Similarly, the "peak_col" denotes horizental distance, in pixel and can be floating point number, from peak center to left edge of the frame. 

## configuration and hyper-parameters

* all hyper parameters and model configurations are given by using augment passing. 
* Please refer the help of main.py, e.g., run python main.py --help to get explaination of each augment
* Once the training process is done, you are encouraged to check the validation error in the log file to find the best model checkpoint. 