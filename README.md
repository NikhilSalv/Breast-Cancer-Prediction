# Breast-Cancer-Prediction
In this is Data model, we are going to implement predictive analytics using R to diagnose whether or not the person has breast cancer based on past medical data.  The data set is collected from the university of California website consisting of breast cancer cases and this is data set will be used to build predictive model to classify a human as a malignant or benign based of certain feature variables.
The link to the data set is below
https://archive.ics.uci.edu/ml/datasets.php
Following are the feature variables of the data set. 
1.	Clump Thickness
2.	Uniformity of Cell Size
3.	Uniformity of Cell Shape
4.	Marginal Adhesion
5.	Single Epithelial Cell Size
6.	Bare Nuclei
7.	Bland Chromatin
8.	Normal Nucleoli
9.	Mitoses
10.	Class

Data munging
Initially the column names of data set were unrecognizable, so that is why we replaced the column names by relevant names which were given in the data description file. The data set has 9 independent variables and one dependent variable which is “class”. “Class variable is classified into “Malignant”, or “benign”. Bare Nucleoli variable, which was initially a character type variable, has been converted into numeric type data variable. 
Model Building
We have split the data into 4 parts, which are training set, testing set, train outcome and test outcome. 70 % (first 477 rows) of the data is in the training set and remaining is in testing set. 
Then we built KNN algorithm on training set and training outcome. The value of k is set to 21. And we applied this model on testing set and test outcome and stored these outcomes in “predictions”
We created a table of actual test outcomes and predictions and checked the accuracy. The accuracy we got is 100 %.

cancerdata<- read.csv("C:/Users/NIKIL/Desktop/Cancer data/breast-cancer-wisconsin.txt")
> str(cancerdata)
'data.frame':	698 obs. of  11 variables:
 $ X1000025: int  1002945 1015425 1016277 1017023 1017122 1018099 1018561 1033078 1033078 1035283 ...
 $ X5      : int  5 3 6 4 8 1 2 2 4 1 ...
 $ X1      : int  4 1 8 1 10 1 1 1 2 1 ...
 $ X1.1    : int  4 1 8 1 10 1 2 1 1 1 ...
 $ X1.2    : int  5 1 1 3 8 1 1 1 1 1 ...
 $ X2      : int  7 2 3 2 7 2 2 2 2 1 ...
 $ X1.3    : chr  "10" "2" "4" "1" ...
 $ X3      : int  3 3 3 3 9 3 3 1 2 3 ...
 $ X1.4    : int  2 1 7 1 7 1 1 1 1 1 ...
 $ X1.5    : int  1 1 1 1 1 1 1 5 1 1 ...
 $ X2.1    : int  2 2 2 2 4 2 2 2 2 2 ...
# Lable the Data set
> names(cancerdata)<- c("id","Clump Thickness","Uniformity of Cell Size" ,"Uniformity of Cell Shape","Marginal Adhesion", 
+                       "Single Epithelial Cell Size","Bare Nuclei","Bland Chromatin","Normal Nucleoli","Mitoses","class")

# Data preparation
> cancerdata$id<- NULL

#Converting data into numeric format

> cancerdata$`Bare Nuclei`<- as.numeric(cancerdata$`Bare Nuclei`)
Warning message:
NAs introduced by coercion 
# Identify rows without missing data

> cancerdata <- cancerdata[complete.cases(cancerdata),]
> cancerdata$class <- factor(ifelse(cancerdata$class == 2, "benign","malignant"))
> trainingSet <-cancerdata[1:477,1:9]
> testset <- cancerdata[478:682,1:9]
> 
> trainOutcomes <- cancerdata[1:477,10]
> testOutcomes <- cancerdata[478:682,10]
# Apply KNN algorithm to training set and training outcome
> 
> library(class)
> predictions <- knn(train = trainingSet, cl = trainOutcomes,k = 21, 
+                    test = testset)
> 
# Display predictions 
> predictions
  [1] malignant benign    benign    benign    benign    benign    benign   
  [8] benign    benign    benign    benign    benign    benign    malignant
 [15] benign    benign    benign    benign    benign    benign    benign   
 [22] malignant malignant benign    benign    benign    malignant benign   
 [29] benign    malignant malignant benign    benign    benign    benign   
 [36] benign    benign    malignant benign    benign    benign    benign   
 [43] benign    benign    benign    benign    benign    benign    benign   
 [50] benign    benign    benign    benign    malignant benign    benign   
 [57] malignant benign    benign    benign    benign    benign    benign   
 [64] benign    benign    benign    benign    benign    benign    benign   
 [71] benign    benign    malignant benign    benign    malignant malignant
 [78] malignant malignant benign    benign    malignant benign    benign   
 [85] benign    benign    benign    benign    malignant malignant benign   
 [92] benign    benign    malignant benign    malignant benign    malignant
 [99] malignant malignant benign    malignant benign    benign    benign   
[106] benign    benign    benign    benign    benign    malignant malignant
[113] malignant benign    benign    malignant benign    malignant malignant
[120] malignant benign    benign    benign    benign    benign    benign   
[127] benign    benign    benign    benign    benign    benign    malignant
[134] benign    benign    benign    benign    benign    benign    malignant
[141] benign    benign    malignant benign    benign    benign    benign   
[148] benign    benign    benign    benign    benign    benign    benign   
[155] malignant benign    benign    benign    benign    benign    benign   
[162] benign    benign    benign    malignant benign    benign    benign   
[169] benign    benign    benign    benign    benign    benign    malignant
[176] malignant malignant benign    benign    benign    benign    benign   
[183] benign    benign    benign    benign    malignant malignant benign   
[190] benign    benign    benign    benign    benign    benign    benign   
[197] benign    malignant benign    benign    benign    benign    malignant
[204] malignant malignant
Levels: benign malignant
> 
# Model evaluation 
> table(testOutcomes, predictions)
            predictions
testOutcomes benign malignant
   benign       160         0
   malignant      0        45
> actuals_pred <- data.frame(cbind(actuals = testOutcomes,predicted = predictions))
> correlation_accuracy <- cor(actuals_pred)
> head(actuals_pred)
  actuals predicted
1       2         2
2       1         1
3       1         1
4       1         1
5       1         1
6       1         1
> correlation_accuracy
          actuals predicted
actuals         1         1
predicted       1         1
> 
> cancerdata<- read.csv("C:/Users/NIKIL/Desktop/Cancer data/breast-cancer-wisconsin.txt")
> str(cancerdata)
'data.frame':	698 obs. of  11 variables:
 $ X1000025: int  1002945 1015425 1016277 1017023 1017122 1018099 1018561 1033078 1033078 1035283 ...
 $ X5      : int  5 3 6 4 8 1 2 2 4 1 ...
 $ X1      : int  4 1 8 1 10 1 1 1 2 1 ...
 $ X1.1    : int  4 1 8 1 10 1 2 1 1 1 ...
 $ X1.2    : int  5 1 1 3 8 1 1 1 1 1 ...
 $ X2      : int  7 2 3 2 7 2 2 2 2 1 ...
 $ X1.3    : chr  "10" "2" "4" "1" ...
 $ X3      : int  3 3 3 3 9 3 3 1 2 3 ...
 $ X1.4    : int  2 1 7 1 7 1 1 1 1 1 ...
 $ X1.5    : int  1 1 1 1 1 1 1 5 1 1 ...
 $ X2.1    : int  2 2 2 2 4 2 2 2 2 2 ...
# lable the Data set
> names(cancerdata)<- c("id","Clump Thickness","Uniformity of Cell Size" ,"Uniformity of Cell Shape","Marginal Adhesion", 
+                       "Single Epithelial Cell Size","Bare Nuclei","Bland Chromatin","Normal Nucleoli","Mitoses","class")
> str(cancerdata)
'data.frame':	698 obs. of  11 variables:
 $ id                         : int  1002945 1015425 1016277 1017023 1017122 1018099 1018561 1033078 1033078 1035283 ...
 $ Clump Thickness            : int  5 3 6 4 8 1 2 2 4 1 ...
 $ Uniformity of Cell Size    : int  4 1 8 1 10 1 1 1 2 1 ...
 $ Uniformity of Cell Shape   : int  4 1 8 1 10 1 2 1 1 1 ...
 $ Marginal Adhesion          : int  5 1 1 3 8 1 1 1 1 1 ...
 $ Single Epithelial Cell Size: int  7 2 3 2 7 2 2 2 2 1 ...
 $ Bare Nuclei                : chr  "10" "2" "4" "1" ...
 $ Bland Chromatin            : int  3 3 3 3 9 3 3 1 2 3 ...
 $ Normal Nucleoli            : int  2 1 7 1 7 1 1 1 1 1 ...
 $ Mitoses                    : int  1 1 1 1 1 1 1 5 1 1 ...
 $ class                      : int  2 2 2 2 4 2 2 2 2 2 ...
# Data preparation
> cancerdata$id<- NULL
# Converting data into numeric format
> cancerdata$`Bare Nuclei`<- as.numeric(cancerdata$`Bare Nuclei`)
Warning message:
NAs introduced by coercion 
> #identify rows without missing data
> cancerdata <- cancerdata[complete.cases(cancerdata),]
> str(cancerdata)
'data.frame':	682 obs. of  10 variables:
 $ Clump Thickness            : int  5 3 6 4 8 1 2 2 4 1 ...
 $ Uniformity of Cell Size    : int  4 1 8 1 10 1 1 1 2 1 ...
 $ Uniformity of Cell Shape   : int  4 1 8 1 10 1 2 1 1 1 ...
 $ Marginal Adhesion          : int  5 1 1 3 8 1 1 1 1 1 ...
 $ Single Epithelial Cell Size: int  7 2 3 2 7 2 2 2 2 1 ...
 $ Bare Nuclei                : num  10 2 4 1 10 10 1 1 1 1 ...
 $ Bland Chromatin            : int  3 3 3 3 9 3 3 1 2 3 ...
 $ Normal Nucleoli            : int  2 1 7 1 7 1 1 1 1 1 ...
 $ Mitoses                    : int  1 1 1 1 1 1 1 5 1 1 ...
 $ class                      : int  2 2 2 2 4 2 2 2 2 2 ...
> cancerdata$class <- factor(ifelse(cancerdata$class == 2, "benign","malignant"))
> trainingSet <-cancerdata[1:477,1:9]
> testset <- cancerdata[478:682,1:9]
> trainOutcomes <- cancerdata[1:477,10]
> testOutcomes <- cancerdata[478:682,10]
> library(class)
> predictions <- knn(train = trainingSet, cl = trainOutcomes,k = 21, 
+                    test = testset)
# Display predictions 
> predictions
  [1] malignant benign    benign    benign    benign    benign    benign   
  [8] benign    benign    benign    benign    benign    benign    malignant
 [15] benign    benign    benign    benign    benign    benign    benign   
 [22] malignant malignant benign    benign    benign    malignant benign   
 [29] benign    malignant malignant benign    benign    benign    benign   
 [36] benign    benign    malignant benign    benign    benign    benign   
 [43] benign    benign    benign    benign    benign    benign    benign   
 [50] benign    benign    benign    benign    malignant benign    benign   
 [57] malignant benign    benign    benign    benign    benign    benign   
 [64] benign    benign    benign    benign    benign    benign    benign   
 [71] benign    benign    malignant benign    benign    malignant malignant
 [78] malignant malignant benign    benign    malignant benign    benign   
 [85] benign    benign    benign    benign    malignant malignant benign   
 [92] benign    benign    malignant benign    malignant benign    malignant
 [99] malignant malignant benign    malignant benign    benign    benign   
[106] benign    benign    benign    benign    benign    malignant malignant
[113] malignant benign    benign    malignant benign    malignant malignant
[120] malignant benign    benign    benign    benign    benign    benign   
[127] benign    benign    benign    benign    benign    benign    malignant
[134] benign    benign    benign    benign    benign    benign    malignant
[141] benign    benign    malignant benign    benign    benign    benign   
[148] benign    benign    benign    benign    benign    benign    benign   
[155] malignant benign    benign    benign    benign    benign    benign   
[162] benign    benign    benign    malignant benign    benign    benign   
[169] benign    benign    benign    benign    benign    benign    malignant
[176] malignant malignant benign    benign    benign    benign    benign   
[183] benign    benign    benign    benign    malignant malignant benign   
[190] benign    benign    benign    benign    benign    benign    benign   
[197] benign    malignant benign    benign    benign    benign    malignant
[204] malignant malignant
Levels: benign malignant
# Model evaluation 
> table(testOutcomes, predictions)
            predictions
testOutcomes benign malignant
   benign       160         0
   malignant      0        45
> actuals_pred <- data.frame(cbind(actuals = testOutcomes,predicted = predictions))
> correlation_accuracy <- cor(actuals_pred)
> head(actuals_pred)
  actuals predicted
1       2         2
2       1         1
3       1         1
4       1         1
5       1         1
6       1         1
> correlation_accuracy
          actuals predicted
actuals         1         1
predicted       1         1
> 
> View(correlation_accuracy)
# Model evaluation 
> table(testOutcomes, predictions)
            predictions
testOutcomes benign malignant
   benign       160         0
   malignant      0        45
> View(data.frame(testOutcomes, predictions))
