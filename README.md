# Getting-and-Cleaning-Data-Course-Project

setwd("D:/For Consulting/Getting and Cleaning Data")
# Read test and train data
subject_test = read.csv("./UCI HAR Dataset/test/subject_test.txt", sep = "", header = FALSE)
y_test = read.csv("./UCI HAR Dataset/test/y_test.txt", sep = "", header = FALSE)
X_test = read.csv("./UCI HAR Dataset/test/X_test.txt", sep = "", header = FALSE)

subject_train = read.csv("./UCI HAR Dataset/train/subject_train.txt", sep = "", header = FALSE)
y_train = read.csv("./UCI HAR Dataset/train/y_train.txt", sep = "", header = FALSE)
X_train = read.csv("./UCI HAR Dataset/train/X_train.txt", sep = "", header = FALSE)

features = read.csv("./UCI HAR Dataset/features.txt", sep = "", header = FALSE)
activity_labels = read.csv("./UCI HAR Dataset/activity_labels.txt", sep = "", header = FALSE)

# Names columns by the description from features file
colnames(X_test) = features[,2]
colnames(X_train) = features[,2]

# Merge training and test data sets
X = rbind(X_test, X_train)
y = rbind(y_test, y_train) # activity
s = rbind(subject_test, subject_train)
colnames(y) = "activity"
colnames(s) = "subject#"

# Take subset of measurements on the mean and calculate its standard deviation
X_mean = X[,grep("mean",names(X))]
X_std = X[,grep("std",names(X))]
X_std_mean = cbind(X_std, X_mean)

# Include subject and activity information inside
Xys = cbind(s, y, X_std_mean)
Xys = Xys[order(Xys[,1], Xys[,2]),]

# Calculate average of each measurement based on each activity
Average = NULL
for (i in 1:6){
  ACT = Xys[Xys[,2] == i, ]
  for (j in 1:30){
    Ave = apply(ACT[ACT[,1] == j,3:length(ACT)], 2, mean)
    Average = rbind(Average, Ave)
  }
  Xys[Xys[,2] == i, 2] = as.character(activity_labels[i,2]) # Rename y by using activity names
}

# Name ros of the data set as "activity" + "_" + "subject#"
rownames(Average) = paste(rep(activity_labels[,2], each = 30), 1:30, sep = "_")

# Write data into .csv file
write.csv(Xys, file = "./measurement on mean and std.csv", row.names = FALSE)
write.csv(Average, file = "./Average.csv")
