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
