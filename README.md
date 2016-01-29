# Getting-and-Cleaning-Data-Course-Project
This assignment uses data from the UC Irvine Machine Learning Repository, we use the "Human Activity Recognition Using Smartphones Data Set" as our data source.

The data taken from the website includes lots of measurements, what we use in this project is only part of it, including "subject_train/test", "X_train/test", "y_train/test" and description files in the "UCI HAR Dataset" main folder.

The script was performed to take out meansurement on the mean and standard deviation among all the measurements and create a new tidy dataframe. In this project, it is named as "measurement on the mean and std.csv". And this data set was further processed by calculating the mean value of each measurement for each subject which created a new dataframe. It is named as "Average.csv".
Here is the step:
1. Load the data
2. Merge test and training data
3. Take a subset out from the original data set, the subset contains all the measurement about "mean" and "standard deviation"
4. Label the data set
5. From step 4, we then calculate the mean value of each measurement for each subject and create a new data set.
