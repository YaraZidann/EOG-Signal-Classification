# EOG-Signal-Classification

Introduction: 

Our project is EOG based Arrows interface, which is based on EOG signal to detect eye movement. 

We collected the EOG Dataset then start doing the Data preparation step to divide data into 4 classes (UP,DOWN,RIGHT,LEFT), Then preprocess the prepared data to reduce noise and get the EOG Band, Then the Feature Extraction phase where we extract features like (Statistical Features from raw data, Wavelet Coefficients &Statistical Features from Wavelet Coefficients) from preprocessed signal , Then the last step is to build a Machine learning Model and train it using the Features extracted, for visualization we build and interface consists of 4 arrows (Up arrow, Down arrow, Right arrow, Left arrow) to show the model prediction for EOG test signal. 

 

Steps: 

1)Data Preparation 

Dataset is a files of signals written in Turkish language: 

First, we read data using (read_data fun.) then rename change the files names from Turkish names to English using (rename_files fun.) and finally remove any files that don’t refer to any EOG signs (up, down, blink, left, right). 

 

Second, extract 3 columns from data after putting it on DataFrame (labels, signal number, channels). 

 

Third, extract data frame for each sign (vertical, horizontal) then concatenates each vertical with horizontal, then put them all in one data frame (blink, up, down, right, left).   

Fourth, We shuffle dataset then store Label column in Y column and drop it with signal number and channels columns.   

2)Data preprocessing 
Removing DC-Component: (To make signal oscillate around X-Axis) 
Bandpass Filtering:  

-Sampling Rate = 176 

-Low Cutoff Frequency = 0.5 HZ 

-High Cutoff Frequency = 20 HZ 

-Goal: To get EOG band, Noise Reduction and Signal Enhancement.  
Normalization: 

 Normalize data in range [-1,1], so each input signal has similar scale. 


 3)Feature extraction 

In Feature extraction we extract 3 different features. 

1- statistical features from raw data: We calculated the mean, STD,  variance and  Energy, then put it on data frame and used it as a feature for the classifier’s models. 

          

2-Wavelet Coefficients: 

We get wavelet coefficients of Normalized signal using 2 levels. 

 

3- statistical features from Wavelet: 

Same calculations in statistical from raw data but we calculated them from 

 wavelet coefficients with 2 levels. 

 4)Models and its parameters 

        (80% Train Data, 20% Test Data) 

Logistic Regression: 

Parameters: 

Penalty: 'l2' or None 

Solver: 'lbfgs', 'liblinear', 'saga' 

Regularization parameter (C): Uniformly distributed between 0 and 4 

 

 

Support Vector Machine (SVM): 

Parameters: 

Kernel: RBF (default) 

Regularization parameter (C) 

 

Gradient Boosting: 

Parameters: 

Loss function: 'deviance' (logistic regression) or 'exponential' 

Learning rate: Uniformly distributed between 0 and 1. 

Max depth of the individual regression estimators: 3 to 8 

Number of boosting stages: 100 to 280 (increments of 20) 

Minimum number of samples required to split an internal node: Uniformly distributed. 

Minimum number of samples required to be at a leaf node: Uniformly distributed. 

Maximum number of features: Uniformly distributed. 

 

Random Forest: 

Parameters: 

Number of trees in the forest: 100, 200, 300, 400, 500 

Maximum depth of the tree: 5, 10, 15, 20, 25, 30, None 

Minimum number of samples required to split an internal node: 2, 5, 10. 

Minimum number of samples required to be at a leaf node: 1, 2, 4. 

Method of selecting samples for training each tree: With or without replacement 

 

Gaussian Naive Bayes: 

Parameters: 

Variance smoothing: Uniformly distributed. 

5)Models Comparison  

 

Performance Comparison for Statistical Features from Raw Data: 

Model 

Accuracy 

F1 Score 

Logistic Regression 

0.55 

0.521667 

SVM 

0.35 

0.361136 

Gradient Boosting 

0.50 

0.490549 

Random Forest 

0.50 

0.531090 

Gaussian NB 

0.50 

0.531923 

 

Performance Comparison for Wavelet Features: 

Model 

Accuracy 

F1 Score 

Logistic Regression 

0.80 

0.81 

SVM 

1.0 

1.0 

Gradient Boosting 

1.0 

1.0 

Random Forest 

0.85 

0.86 

Gaussian NB 

0.75 (Best Prediction) 

0.7475 

 

Performance Comparison for Statistical Wavelet Features: 

Model 

Accuracy 

F1 Score 

Logistic Regression 

0.45 

0.440303 

SVM 

0.35 

0.361136 

Gradient Boosting 

0.50 

0.488214 

Random Forest 

0.55 

0.559780 

Gaussian NB 

0.50 

0.531923 

 6)Interface:
 Components: 

     1- Directional Buttons: 

Up, down, left, right and blink directional buttons for simulating eye movements. 

Each button triggers a color change to indicate the direction of the simulated eye movement. 

Text: Unicode arrows (↑, ↓, ←, →) 

Behavior: 

The second window remains open until the user closes it manually. 

Upon closing, the second window returns to the main window. 
 Components: 

      1- Upload Data Button: 

Upon clicking, you can upload your test file then it opens the second window for data interaction. 

 

      2- Model Selection Dropdown (Combo Box): 

 Allows the user to select a trained model from a list of available models. 

 Behavior: 

Users can interact with the main window to select a model and initiate data upload. 
