GettingAndCleaningDataCourse
============================

For course in Data Science track

run_analysis.r script explanation:

#load the various datasets
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt", quote="\"")

subject_test <- read.table("./UCI HAR Dataset/test/subject_test.txt", quote="\"")

X_test <- read.table("./UCI HAR Dataset/test/X_test.txt", quote="\"")

y_test <- read.table("./UCI HAR Dataset/test/y_test.txt", quote="\"")

features <- read.table("./UCI HAR Dataset/features.txt", quote="\"")

#name the variables in X_test dataset using features
names(X_test)<-features$V2

#add subjects variable to X_test using cbind function and subject_test dataset
X_test_s<-cbind(subject_test,X_test)

#name V1 of X_test_s
names(X_test_s)[1]<-"Subject"

subject_train <- read.table("./UCI HAR Dataset/train/subject_train.txt", quote="\"")

X_train <- read.table("./UCI HAR Dataset/train/X_train.txt", quote="\"")

y_train <- read.table("./UCI HAR Dataset/train/y_train.txt", quote="\"")

#name the variables in X_train dataset using features
names(X_train)<-features$V2

#add subjects variable to X_train using cbind function and subject_train dataset
X_train_s<-cbind(subject_train,X_train)

#name V1 of X_train_s
names(X_train_s)[1]<-"Subject"


#merge X_test and X_train to form "X_complete" using rbind function
X_complete<-rbind(X_train_s,X_test_s)

#extract only measurements on mean and standard deviation
meanVars<-grep("mean()",names(X_complete))
stdVars<-grep("std()",names(X_complete))
RelevantVars<-c(1,meanVars,stdVars)

X_tidy<-X_complete[,RelevantVars]

#export tidy dataset text file
write.table(X_tidy, "./Course_Project_TidyData.txt", sep="\t") 

