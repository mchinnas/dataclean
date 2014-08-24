## README.md for the Data Cleanup project. 

#### The original document, the datasets and other details can be found at the coursera link

https://class.coursera.org/getdata-006/human_grading/view/courses/972584/assessments/3/submissions

###This github repository contains following files

The R script run_analysis.R
A README.md & CodeBook.md files
A tidy dataset dataset.txt - output file from step 5

###Assumptions

It assumes that the reader is aware of the course project and the original datasets involved.
Also assumed that the dataset zip file is extracted into your workspace. So you would have "workspace/UCI HAR Dataset" and its contents

## High level process conducted to clean up the data and make it tidy
1. Read all test/X_test.txt,  test/y_test.txt, test/subject_test.txt
2. Merge all the three by column wise
3. Similarly the train files
4. Merge the column merged test and train files
5. Column 1 & 2 will have 'subject', 'activity' as headings
6. Read the feature.txt file and assign to the remaing columns of the above merged file.
7. Read the activity label file and assign to the activity column in the above merged file
8. Extract only columns which has mean or std and drop the remaining columns.
9. This script need the reshape2 packages apart from the standard packages
10. Using the reshape2 package calculate the average of each variable for each activity and each subject
11. Write the result to dataset.txt

##The Following is the R-script code with comments

## Read all three test data
xtest.data <-read.table("UCI HAR Dataset/test/X_test.txt", numerals = "no.loss")

ytest.data <-read.table("UCI HAR Dataset/test/y_test.txt")

subject.test.data <-read.table("UCI HAR Dataset/test/subject_test.txt")

## Change the variable name
names(ytest.data) <- c("activity")
names(subject.test.data) <- c("subject")

## Merge all three tets dataset by column wise
test.data <- cbind(subject.test.data, ytest.data, xtest.data)

## Read all three training datasets
xtrain.data <-read.table("UCI HAR Dataset/train/X_train.txt", numerals = "no.loss")

ytrain.data <-read.table("UCI HAR Dataset/train/y_train.txt")

subject.train.data <-read.table("UCI HAR Dataset/train/subject_train.txt")

## Change the variable names
names(subject.train.data) <- c("subject")

names(ytrain.data) <- c("activity")

## Merge all three training dataset by column wise
train.data <- cbind(subject.train.data, ytrain.data, xtrain.data)

## Merge the training and test datasets by rowise
merged.data <- rbind(test.data, train.data)

## Read the features dataset
feature.data <- read.table("UCI HAR Dataset/features.txt")

## Name the columns
names(feature.data) <- c("columnno", "columnname")

## Add columns for the merged.data dataset
valid.headings <- as.vector(feature.data$columnname)
final.headings <- append(c("subject", "activity"), valid.headings)

## Assign the names 
names(merged.data) <- final.headings

## Find out the columns which has mean or std and club together
mean.columns <- as.vector(grep("mean", names(merged.data)))

std.columns <- as.vector(grep("std", names(merged.data)))

mean.std.columns <- append(mean.columns, std.columns)

## Add with the subject, activity columns
all.columns <- append(c(1,2) ,mean.std.columns)

## Get the required data in the order
final.data <- merged.data[,sort(all.columns)]

## Read the activity label file and assign to the activity column in final.data
activity.label.data <- read.table("UCI HAR Dataset/activity_labels.txt")

final.data[,2] <- activity.label.data[final.data$activity,2]

## Remove the '-' and '()' symbols from the column headings
names(final.data) <- tolower(gsub("-|\\()", "", names(final.data)))

## The script needs 'reshap2' package
require(reshape2)

## Meltdown/reshape the dataset with three columns
final.data.melt <- melt(final.data, id = c( "subject", "activity"))

## Find the mean for all column variables in thrird column
result.data <- dcast(final.data.melt, subject + activity ~ variable, mean)

## Write the result to an output file.
write.table(result.data, file = "dataset2.txt", sep = " ")
