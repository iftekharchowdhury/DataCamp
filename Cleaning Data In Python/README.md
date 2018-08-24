# Loading and viewing your data
In this chapter, you're going to look at a subset of the Department of Buildings Job Application Filings dataset from 
the NYC Open Data portal. This dataset consists of job applications filed on January 22, 2017.
Your first task is to load this dataset into a DataFrame and then inspect it using the .head() 
and .tail() methods. However, you'll find out very quickly that the printed results don't allow
you to see everything you need, since there are too many columns. Therefore, you need to look at
the data in another way. The .shape and .columns attributes let you see the shape of the DataFrame
and obtain a list of its columns. From here, you can see which columns are relevant to the questions 
you'd like to ask of the data. To this end, a new DataFrame, df_subset, consisting only of these relevant
columns, has been pre-loaded. This is the DataFrame you'll work with in the rest of the chapter.
Get acquainted with the dataset now by exploring it with pandas.This initial exploratory analysis is a crucial first step of data cleaning.

## Instructions

* Import pandas as pd.
* Read 'dob_job_application_filings_subset.csv' into a DataFrame called df.
* Print the head and tail of df.
* Print the shape of df and its columns. Note: .shape and .columns are attributes, not methods, so you don't need to follow these with parentheses ().
* Hit 'Submit Answer' to view the results! Notice the suspicious number of 0 values. Perhaps these represent missing data.

```python

# Import pandas
import pandas as pd

# Read the file into a DataFrame: df
df = pd.read_csv('dob_job_application_filings_subset.csv')
# Print the head of df
print(df.head())

# Print the tail of df
print(df.tail())

# Print the shape of df
print(df.shape)

# Print the columns of df
print(df.columns)

# Print the head and tail of df_subset
print(df_subset.head())
print(df_subset.tail())
```
# Further diagnosis
In the previous exercise, you identified some potentially unclean or missing data. Now, you'll continue to diagnose your data with the very useful .info() method. The .info() method provides important information about a DataFrame, such as the number of rows, number of columns, number of non-missing values in each column, and the data type stored in each column. This is the kind of information that will allow you to confirm whether the 'Initial Cost' and 'Total Est. Fee' columns are numeric or strings. From the results, you'll also be able to see whether or not all columns have complete data in them. 
The full DataFrame df and the subset DataFrame df_subset have been pre-loaded. Your task is to use the .info() method on these and analyze the results.

```python

# Print the info of df
print(df.info())
# Print the info of df_subset
print(df_subset.info())
```
# Calculating summary statistics

You'll now use the .describe() method to calculate summary statistics of your data.
In this exercise, the columns 'Initial Cost' and 'Total Est. Fee' have been cleaned up for you. That is, the dollar sign has been removed and they have been converted into two new numeric columns: initial_cost and total_est_fee. You'll learn how to do this yourself in later chapters. It's also worth noting that some columns such as Job # are encoded as numeric columns, but it does not make sense to compute summary statistics for such columns.
This cleaned DataFrame has been pre-loaded as df. Your job is to use the .describe() method on it in the IPython Shell and select the statement below that is False.

# Frequency counts for categorical data

As you've seen, .describe() can only be used on numeric columns. So how can you diagnose data issues when you have categorical data?
One way is by using the .value_counts() method, which returns the frequency counts for each unique value in a column!
This method also has an optional parameter called dropna which is True by default. What this means is if you have missing data in a column, it will not give a frequency count of them. You want to set the dropna column to False so if there are missing values in a column, it will give you the frequency counts.
In this exercise, you're going to look at the 'Borough', 'State', and 'Site Fill' columns to make sure all the values in there are valid. When looking at the output, do a sanity check: Are all values in the 'State' column from NY, for example? Since the dataset consists of applications filed in NY, you would expect this to be the case.

```python

# Print the value counts for 'Borough'
print(df['Borough'].value_counts(dropna=False))

# Print the value_counts for 'State'
print(df['State'].value_counts(dropna=False))

# Print the value counts for 'Site Fill'
print(df['Site Fill'].value_counts(dropna=False))
```




































