UW-EE399-Assignment-6
=========
This holds the code and backing for the sixth assignment of the EE399 class. The main dataset this assignment revolves around is Sea Surface Temperatures collected globally. These data are fed into a Shallow Recurrent Decoder to demonstrate the extrapolation capabilities of neural network models.

Project Author: Elijah Reeb, elireeb@uw.edu, Other Authors cited at bottom

.. contents:: Table of Contents

Homework 6
---------------------
Introduction
^^^^^^^^^^^^
This assignment involves hyperparameter tuning around written code on Sea Surface Temperature (SST) data. This assignment involves determining the extent to which a model is able to recreate a model using very minimal input data points. Much of this code was written by others and can be originally found at https://github.com/Jan-Williams/pyshred. 

.. image:: https://github.com/ElijahReeb/UW-EE399-Assignment-6/assets/130190276/8b5222d5-20f1-4172-a475-6f2b9142d522

Theoretical Backgroud
^^^^^^^^^^^^
Many applications in electrical engineering revolve around collection of data from the world or a device or a system via use of sensors. However, sometimes very limited amounts of sensors are avaiable to read from and yet a large amount of area is expected. This assignment revolves around the example of mapping the surface temperature of the ocean. With a very minimal amount of sensors, the use of a model can be used to miraculously map a massive area with minimal error. 
The theoretical model used is a decoder neural network. This means minimal nodes are translated into a large array of output. This is shown on the right of the image below from pathmind.com. The autoencoder network on the left does the opposite taking large amounts of data and reducing to the more necessary dimensions. These models can be very helpful when paired together with each other or used to preprocess as set up a different model.

.. image:: https://github.com/ElijahReeb/UW-EE399-Assignment-6/assets/130190276/08157919-562d-4986-b985-7c23f1b0b623

Algorithm Implementation and Development
^^^^^^^^^^^^
The main algorithm behind this assignment is the SHRED model. This is a Shallow Recurrent Decoder method. Similar to many other assignments, much of the model code is not in the file worked with but set up in the back end with hyperparameters passed and then fit to data. The simple line of code below shows what is necessary to set up this decoder model. Note that a larger amount of preprocessing may be necessary for the data, but to create the model only the line below is needed.

.. code-block:: text
  
     shred = models.SHRED(num_sensors, m, hidden_size=64, hidden_layers=2, l1=350, l2=400, dropout=0.1).to(device)

From examination of this line of code we are able to determine the decoding basis. The num_sensors is the first small layer that is the input. The hidden layers are much larger at 64 and then moving to 350 and 400. This shows the massive extrapolation from 3 or so to 400. Additionally, less relevant to this model in particular, but this model uses a dropout stage. This means that some amount of the weights are just randomly set to 0. This helps to reduce over tuning of the model. 

Computational Results
^^^^^^^^^^^^
Next the hyperparameters will be the focus. When observing the results of training this model the starting values of 3 sensors and a lag of 52 was used. The results of training that model are plotted below. One can observe that after about 200 epochs there was not as much improvement. This model took a very long time to run so 100 less epochs could save 15 minutes.

.. image:: https://github.com/ElijahReeb/UW-EE399-Assignment-6/assets/130190276/f50cae4b-cecc-4dab-b137-4f73eaa8e603

This use of 200 epochs was used for the later testing. Three main parameters were focused on. The number of sensors which was varied from 1 to 8. The amount of lag in the data which was varied over the interval 1 to 100. And last, while not a parameter, a level of noise was added to the data. Comparing the training graphs for these three situations, there is not a massive difference. 

.. image:: https://github.com/ElijahReeb/UW-EE399-Assignment-6/assets/130190276/82e19c92-eca9-4c22-a082-bb3081d54d01


Finally after training the models under different parameters the data was compared to a ground truth dataset to determine the overall error of the model. Those are plotted below in the bar graphs and will be discussed later. We are able to see relatively similar error around 0.03.

.. image:: https://github.com/ElijahReeb/UW-EE399-Assignment-6/assets/130190276/6d2ce65e-5ac4-4f62-9a9c-1804b54a95de


Summary and Conclusions
^^^^^^^^^^^^



Previous ReadMe from Previous Authors
^^^^^^^^^^^^
This repository contains the code for the paper "Sensing with shallow recurrent decoder networks" by Jan P. Williams, Olivia Zahn, and J. Nathan Kutz. SHallow REcurrent Decoders (SHRED) are models that learn a mapping from trajectories of sensor measurements to a high-dimensional, spatio-temporal state. For an example use of SHRED, see the iPython notebook example.ipynb.

The datasets considered in the paper "Sensing with shallow recurrent decoder networks" consist of sea-surface temperature (SST), a forced turbulent flow, and atmospheric ozone concentration. Cloning this repo will download the SST data used. Details for accessing the other datasets can be found in the supplement to the paper. 

Note additional collaboration with Najib H
