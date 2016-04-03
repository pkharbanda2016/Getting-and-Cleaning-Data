Overview

This repository contains R code that accomplishes the tasks given in the "Getting and Cleaning Data Course Project"

Getting and Cleaning Data Course Project - original course assignment:


The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected. 

One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained: 

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

Here are the data for the project: 

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

You should create one R script called run_analysis.R that does the following. Merges the training and the test sets to create one data set. Extracts only the measurements on the mean and standard deviation for each measurement. Uses descriptive activity names to name the activities in the data set Appropriately labels the data set with descriptive variable names. Creates a second, independent tidy data set with the average of each variable for each activity and each subject. Good luck!

Source: https://class.coursera.org/getdata-006/human_grading/index

R script run_analysis.R abstract:

1.Merges the training and the test sets to create one data set.
2.Extracts only the measurements on the mean and standard deviation for each measurement. 
3.Uses descriptive activity names to name the activities in the data set
4.Appropriately labels the data set with descriptive variable names. 
5.Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

Source: https://class.coursera.org/getdata-006/human_grading/index

R script run_analysis.R details:

Preparation

Function:  DownloadData.set(url) 

Check if folder "data" exists in working directory, or create it. Download and extract the zip file containing the dataset FUCI HAR Dataset.zip into folder "data"

1. Loading and Merging the test sets

Function:  LoadMergeData() 

Following the assignment both training and test data sets shall be merged. Due to the fact that they reside in different subfolders the script addresses this while concatenating the common path with the individual subfolder and filenames into global value "path". Load the main file  X_train.txt  (resp.  X_test.txt ) into a data frame train.dat ( resp. test.dat ) then append the  Y_train.txt ( resp.  Y_test.txt ) and subject_train.txt(resp.  subject_test.txt ) to the data frames using read.csv() Once all measurements are loaded, the two data frames train.dat and test.dat can be merged into a single data frame 

return result

2. Variable Selection

Function:  ExtractData(df) 

According to the assignment only the features that contain mean and standard deviation are in scope. Read the file  features.txt  into a global data frame called "features" using read.csv(). Perform a regex search for strings containing "-mean" or "-std" on the features list and store the result in a global vector called cols.in.scope Thus the features in scope are given and the resulting vector can be used to reduce DF "feature" To be able to reduce the DF "Data" add the columns ID for variable "activity" and "subject" to the vector col.in.scope because they need to be kept for later aggregation. Once that's done the col.in.scope vector can be used to remove the obsolete columns out of the input data frame.

return result

3. Use Descriptive activity names (due to script design will be performed after step 4.)

Function:  SetActivityNames(df) 

The activity labels are declared in the file  activity_labels.txt . Load file into a DF "activity.Labels" using read.csv(). Loop through input data frame and replace activity IDs with their matching lables. return result

4. Label the data set with descriptive variable names

Function:  DescriptiveVariables(df) 

Alter the variable names with the use of gsub() function. For better readability and the author choose to make following replacements (following the Rguide):
�substitute "-mean" with ".mean"
�substitute "-std" with ".std"
�substitute "-meanFreq()" with ".mean.freq"
�substitute "-" with "."
�remove "()"
�convert upper to lower case

return result

5. Creating the tidy data set

Function:  MakeTidy(df) 

Declare the variable  activity  and  subject  as noiminal data with R function  as.factor()  To avoid errors on aggregation use subset of DF Data (the columns containing numeric data, which are all except the last two columns  activity  and  subject ) Then aggregate by grouping on "activity" and "subject" calculating the mean for each (numeric) variable and return the result.

Completion

Write global DF Tidy.Data into the file  tidy.txt  using tabs as separators and avoid line numbers.

See  CodeBook.md  for details on result and the variables