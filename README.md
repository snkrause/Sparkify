# Sparkify

### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [Approach](#approach)
4. [Blog](#blog)
5. [Files in the repository](#files)

## Installation <a name="installation"></a>

For the notebook that runs on your local computer there should be no necessary libraries to run the code here beyond the Anaconda distribution of Python.  The code should run with no issues using Python versions 3.\*.

The notebooks that start with "AWS_" are the versions that run on the EMR cluster on Amazon Web Services (AWS). Those need an EMR cluster with a "PySpark" kernel. The details on how to set up the EMR cluster and the EMR notebook can be found at this link: https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks.html

Any missing python libraries will be installed with the code in the beginning of the notebook.

## Project Motivation<a name="motivation"></a>
This project is part of my udacity Nanodegree Data Science. It is set to show a big data use-case with a large dataset of about 14.5 GB hosted on a S3 on AWS. This dataset is the user logs of a fictive music streaming service called "Sparkify" and the task is to establish a machine learning model that predicts if a user is canceling the service (called "churn"). Furthermore, I used visualizations to explore trends in a large dataset like this and this way also find hints on way and when users are dropping out.

## Approach<a name="approach"></a>

### 1. Checking a sample dataset
Each students gets a sample dataset of about 120 MB that is small enough to process it on their local machine. With this dataset I could get familiar with the differences of PySpark and Python in coding and approaching solutions. I created the Jupyter notebook "Sparkify_Explore_Data.ipynb" to first explore the data. Here I wanted to know:

- what are the features in the data?
- what is their statistics and unique values?
- how do I clean this dataset?
- in particular the feature "page" is interesting because it contains all the user actions - what are all those actions?
- how can I define that a user dropped out?

The page action of "submit cancellation" could be used to define a user dropping out. The dataset did have a time axis "ts", but I defined a mutual relative time axis "membership_days" to see how the users are evolving over the time of their membership. In order to learn more about general trends in the data I also created the feature "week" that allows me to aggregate indicators over it and visualize trends. More about this in the blog that is linked in this README.

I the second notebook "Sparkify_ML.ipynb" I further wrangeled the data and provide a dataframe that has aggregated features by "userId". The dataset is strongly imbalanced which is why I tried a "Decision Tree Classifier" (dtc) and a "Random Forest Classifier" (rfc) to predict if a user "churns" or not. Both of those algorithms are known to be good with imbalanced datasets. The rfc yielded better results and was therefore chosen for a hyperparameter tuning. At the beginning of this notebook I defined a function to measure the performance of each model witht the basic definitions of accuracy, precision, f1, and recall. It also includes a confusion matrix which I did not find as a function in the pyspark library. Again you can find the details in my blog article.

### 2. Moving it to AWS
This step needed a little research on top of the information that is provided by udacity to set up an EMR cluster with a notebook. A particular problem was for me that my work laptop did not allow me (company policies) to upload data to the S3 or even save my notebooks there. Only after switching to my personal computer could I do those things and really work on my project.
The EMR notebook with a Pyspark kernel also posed some challenges because it was lacking crucial libraries like "pandas" or "matplotlib", which I needed to visualize my data. A little search on AWS helped solving this problem and the link provided in the "installation" section will also help with this. There is a pip installer available and some "magic methods" to plot your data.
After solving those issues I could basically transfer my notebooks that I developed on the sample dataset. I had a couple of glitches in my code where my approach was too memory consuming to run on the EMR cluster but that was fixed quickly.
All of the results on the small dataset were confirmed and the already observed trends got mor clear.

## Blog <a name="blog"></a>


## Files in the repository <a name="files"></a>

    files
    |- AWS__Sparkify_Explore_Data.ipynb # Jupyter notebook for EMR cluster for data exploration
    |- AWS__Sparkify_Explore_Data.html # html version of AWS data exploration
    |- AWS__Sparkify_ML.ipynb # Jupyter notebook for EMR cluster with ML modelling
    |- AWS__Sparkify_ML.html # html version of AWS ML modelling
    |- Sparkify_Explore_Data.ipynb # Jupyter notebook for data exploration
    |- Sparkify_Explore_Data.html # html version data exploration
    |- Sparkify_ML.ipynb # Jupyter notebook with ML modelling
    |- Sparkify_ML.html # html version of ML modelling
    |- categoricals.xlsx # list of unique values of feature "page" (small dataset)
    |- unique_values.xlsx # count of occurences of each unique value in "page" (small dataset)
    |- string_col_values.xlsx # unique values of all categorial features (small dataset)
    |- random_forest_hyperparameter_results.xlsx # results of f1 values for all parameter permutations in rfc (small dataset)
    |- README.md
    |- LICENSE 
