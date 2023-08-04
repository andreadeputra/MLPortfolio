# Predict Customer Clicked Ads Classification by Using Machine Learning
This project is part of Rakamin Academy's portfolio building. In this project, I am given a dataset about a customer database from a company. This company wants to evaluate the effectiveness of their ads. The goal of this project is to make a machine learning model to solve this company's problem in their marketing effort. 

## Customer Type and Behaviour Analysis on Advertisement
For the first step, I did some quick EDA to analyze the company's customerbase. For this project, the focus on the behaviour analysis will be mostly using the numerical features **Age**, **DailyTimeOnSite**, and **DailyNetUsage**.
The EDA consists of univariate, bivariate, and multivariate analysis. Here are some findings and observations made from these EDA:
- Customers who didn't click on ad are mostly 35 years old or younger
- Customers who spends more time on the internet in general is less likely to click on ad
- Time spent on site is part of internet usage (possible redundancy)
- There is a negative correlation between age and time spent

## Data Cleaning & Preprocessing
In this step, I did some preparation for machine learning by doing data cleaning and preprocessing. Here are the overview of what i did in this step:
- Data Cleaning
- Data Splitting
- Data Transformation and Engineering

### Data Cleaning
In this step, I did another quick overview towards the data at hand. The objective for this step is to prepare the data before splitting it into train and test dataset. Fortunately, there is no duplicates found in this dataset. However there are some missing values and columns datatype that might not be suitable for certain machine learning models. While tree based model might be able to handle categorical values, some algorithm like logistic regression might not be able to. Thus to open for more options in machine learning model, some encoding needs to be done for some columns that already have binary values in 'object' datatype.

Here are the summary of what I did in data cleaning:
- Filling missing values in **DailyTimeOnSite**, **AreaIncome**, **DailyNetUsage**, and **Male** columns based on their distributions
- Validating **Timestamp** column by changing its datatype into datetime
- Extracted year, month, week, and day from **Timestamp**
- Changing values of **Male** to represent binary values
- Changing values of **AdClick** to represent binary values

### Data Splitting
After cleaning the dataset, the data is mostly ready for splitting. The target columns for this dataset will be **AdClick** since the objective was to evaluate ad's effectiveness. After separating target and features, I split the data with 80:20 ratio of train and test dataset. Train-test split is done before further encoding as an attempt to reduce data leakage probability by only fitting to train dataset.

### Feature Transformation and Engineering
After splitting is done, there are still 3 more columns to encode and rescaling to be done. The objective of this step will be to do transformation based on train dataset before using the fitted variable to transform the test dataset. Here are the summary of what I did in this step:
- Encoded **city**, **province**, and **category** using BinaryEncoder
- Normalized 4 numerical columns using Yeo-Johnson Transformation