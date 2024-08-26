# C5_Project_DS_Capstone
Final project for the Data Science Nanodegree of Udacity

### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [File Descriptions](#files)
4. [Instructions](#instructions)
5. [Results](#results)
6. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation<a name="installation"></a>

The code uses the libraries available in the default environment base (root) of Anaconda distribution 2.6.2 under Python 
version 3.11.5. The user only needs to update the library **imblearn** to version **0.12.3**. Additionally, **two folders** in the root directory where the notebooks are copied to need to be created: **data and images**. Finally, the four dataset csv files, **Udacity_AZDIAS_052018.csv, Udacity_CUSTOMERS_052018.csv, Udacity_MAILOUT_052018_TRAIN.csv and Udacity_MAILOUT_052018_TEST.csv** need to be copied to the data folder as well as **DIAS Attributes - Values 2017.xlsx** file. Once done these setps, the code should run with no issues.

## Project Motivation<a name="motivation"></a>

The aim of this project was to analyze the demographics data for customers of a mail-order sales company in Germany, 
comparing it against demographics information for the general population of germany. 
I used a k-means model to perform customer segmentation, identifying the parts of the population that best described the 
core customer base of the company. 
Then, I applied what I had learned on a third dataset with demographics information for targets of a marketing campaign for the company, and used a Gaussian Naive Bayes classificator to predict which individuals were most likely to convert into becoming customers for the company. 
The data that I was using, had been provided by Udacity partners at Bertelsmann Arvato Analytics, and represented a real-life data science task.
The versions of those two datasets used in this project included many more features and had not been pre-cleaned.  So, I applied several cleaning techniques such as dropping outlier rows and columns, re-encode unkown values as missing values or mixed-type values and clustering into a single group those categories representing a low amount of data for the feature, 
among others.

## File Descriptions <a name="files"></a>

The project is split into three notebooks:

1. [C5.1.Arvato_Project_ETL](https://github.com/flopez81/C5_Project_DS_Capstone/blob/main/C5.1.Arvato_Project_ETL.ipynb)
This notebook implements the data exploratory analysis where several cleaning operations have been conducted prior to the 
users segmentation. These operations include in the following order:

- Turning the unknown values into missing values
- Dropping the columns with highest amount of missing values
- Dropping the remaining rows with highest amount of missing values
- Re-encoding the mixed-type features into new ordinal/categorical features
- Reducing the cardinality of the categorical features having categories with low density
- Setting up the binary features by turning them into 0-1 values
- Filling out the remaining missing values with the statistic operator according to the feature type

The cleaning operations were applied the following four datasets:
- Udacity_AZDIAS_052018.csv. This file holds the demographics data for all the population of germany
- Udacity_CUSTOMERS_052018.csv. This file holds only the customers demographics data of Arvato
- Udacity_MAILOUT_052018_TRAIN.csv. This file holds the training dataset of the customers demographics data of Arvato
- Udacity_MAILOUT_052018_TEST.csv. This file holds the test dataset of the customers demographics data of Arvato

These files are not included in the github repository as the owner does not grant permission. Please, ask for a copy of these files directly either to Udacity or the contact person of Arvato. Additionally, the excel files DIAS Attributes - Values 2017.xlsx and DIAS Information Levels - Attributes 2017.xlsx are included. The former is also needed for cleaning the csv files, whereas the latter is for data understanding purposes only. DIAS Attributes - Values 2017.xlsx was formerly given by Udacity without the extra column type, which was added in order to classify the variables and treat them appropriately. 

2. [C5.2.Arvato_Project_Unsupervised_ML] (https://github.com/flopez81/C5_Project_DS_Capstone/blob/main/C5.2.Arvato_Project_Unsupervised_ML.ipynb)
This notebook implements the customer segmentation, identifying the parts of the population that best describes the  core customer base of the company. The cleaned Udacity_AZDIAS_052018.csv and Udacity_CUSTOMERS_052018.csv files are loaded as pickle files that were generated in the previous notebook. On these files, three operations are applied: 
- Featuring scaling (FS)
- Dimensionality reduction (DR)
- Clustering (C)

The FS normalizes the datatsets within the 0-1 range by using a customized robust scaler. Then, the DS reduces the number of users to be clustered using the PCA technique by looking at the explained variance. Finally, the C uses a k-means model to group people into cluster with similar features. The latter allows to find the amounts of germany population and customers held in each cluster and to compare them to see which are underrepresented, which are the ones to focus on. All these operations are implementing using classes, so as to customize them, and embeded into a pipeline which is first fit with the germany cleaned demographics data first, and then used to transform the data and to predict the clusters for both datasets. Several plot techniques are used either to determine some hyperparameters of the pipeline components or to analyze the predicted results.

3. [C5.3.Arvato_Project_Supervised_ML](https://github.com/flopez81/C5_Project_DS_Capstone/blob/main/C5.3.Arvato_Project_Supervised_ML.ipynb)
This notebook implements a classifier to predict which individuals are most likely to convert into becoming customers for the company. The cleaned Udacity_MAILOUT_052018_TRAIN.csv and Udacity_MAILOUT_052018_TEST.csv files are loaded as pickle files that were generated in the first notebook. A exploratory analysis is first conducted showing that the test dataset does not hold the response variable and that the train datatset is extremly imbalanced. Therefore, a SMOTE technique is applied before further analyzing that dataset but after normalizing the data as in the previous notebook. With this 
treatment, four different ML models are fitted (logistic regression, gaussian naive bayes, decision tree and random forest) and determined which one outperforms. A repeated stratified k-folder technique is used to further split the training datatset into smaller training and test datasets. This model is then fine-tuned on a randomized grid search by determining which are the hyperparameters improving the key metric while not worsening too much the other metrics.

## Instructions<a name="instructions"></a>
The following order of execution in jupyter should be carried out in order to get the desired results:
1. Run first the C5.1.Arvato_Project_ETL, no matter which output you want to obtain. You should see 4 created pickles files
in data folder and two png files in images folder. 
2. Run the C5.2.Arvato_Project_Unsupervised_ML, if you want to conduct the users segmentation. You should see 6 png files in images folder.
3. Run the C5.3.Arvato_Project_Supervised_ML, if you want to predict the target users of the campaing to send to the emails You should see 2 png files in images folder.

Steps 2 and 3 can be interchanged as the output would not be affected. However, make sure to create first the data and images folders and copy the corresponding csv files and excel file.

## Results <a name="results"></a>
The main findings of the code can be found at the post available 
[here](https://medium.com/@francesc.lopezr/defining-customer-clusters-and-improving-customer-response-2b6c64e2727e).

## Licensing, Authors, Acknowledgements<a name="licensing"></a>

The project is under a restricted usage of the datatsets. You can find the terms of that Licensing in the 
[LICENSE file](https://github.com/flopez81/C5_Project_DS_Capstone/blob/main/LICENSE). Under these terms, you neither can use the code for analysing the Arvato data nor give credit to that company. 
However, you can use the code to analysing other free available data as you would like!
