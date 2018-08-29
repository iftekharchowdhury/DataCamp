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
# Visualizing single variables with histograms

Up until now, you've been looking at descriptive statistics of your data. One of the best ways to confirm what the numbers are telling you is to plot and visualize the data.
You'll start by visualizing single variables using a histogram for numeric values. The column you will work on in this exercise is    ```Existing Zoning Sqft```.

The **.plot()** method allows you to create a plot of each column of a DataFrame. The kind parameter allows you to specify the type of plot to use - kind='hist', for example, plots a histogram.

In the IPython Shell, begin by computing summary statistics for the 'Existing Zoning Sqft' column using the .describe() method. You'll notice that there are extremely large differences between the min and max values, and the plot will need to be adjusted accordingly. In such cases, it's good to look at the plot on a log scale. The keyword arguments logx=True or logy=True can be passed in to .plot() depending on which axis you want to rescale.

Finally, note that Python will render a plot such that the axis will hold all the information. That is, if you end up with large amounts of whitespace in your plot, it indicates counts or values too small to render.

## Instructions
* Import matplotlib.pyplot as plt.
* Create a histogram of the 'Existing Zoning Sqft' column. Rotate the axis labels by 70 degrees and use a log scale for both axes.
* Display the histogram using plt.show().

```python

# Import matplotlib.pyplot
import matplotlib.pyplot as plt

# Plot the histogram
df['Existing Zoning Sqft'].plot(kind='hist', rot=70, logx=True, logy=True)

# Display the histogram
plt.show()
```
# Visualizing multiple variables with boxplots

Histograms are great ways of visualizing single variables. To visualize multiple variables, boxplots are useful, especially when one of the variables is categorical. 
In this exercise, your job is to use a boxplot to compare the 'initial_cost' across the different values of the 'Borough' column. The pandas .boxplot() method is a quick way to do this, in which you have to specify the column and by parameters. Here, you want to visualize how 'initial_cost' varies by 'Borough'.
pandas and matplotlib.pyplot have been imported for you as pd and plt, respectively, and the DataFrame has been pre-loaded as df.

## Instructions

* using the .boxplot() method of df, create a boxplot of 'initial_cost' across the different values of 'Borough'.
* Display the plot.

```python

# Import necessary modules
import pandas as pd
import matplotlib.pyplot as plt

# Create the boxplot
df.boxplot(column='initial_cost', by='Borough', rot=90)

# Display the plot
plt.show()
```

# Visualizing multiple variables with scatter plots
Boxplots are great when you have a numeric column that you want to compare across different categories. When you want to visualize two numeric columns, scatter plots are ideal.

In this exercise, your job is to make a scatter plot with 'initial_cost' on the x-axis and the 'total_est_fee' on the y-axis. You can do this by using the DataFrame .plot() method with kind='scatter'. You'll notice right away that there are 2 major outliers shown in the plots.

Since these outliers dominate the plot, an additional DataFrame, df_subset, has been provided, in which some of the extreme values have been removed. After making a scatter plot using this, you'll find some interesting patterns here that would not have been seen by looking at summary statistics or 1 variable plots.

When you're done, you can cycle between the two plots by clicking the 'Previous Plot' and 'Next Plot' buttons below the plot.

## Instructions

* Using df, create a scatter plot (kind='scatter') with 'initial_cost' on the x-axis and the 'total_est_fee' on the y-axis. Rotate the x-axis labels by 70 degrees.
* Create another scatter plot exactly as above, substituting df_subset in place of df.

```python

# Import necessary modules
import pandas as pd
import matplotlib.pyplot as plt

# Create and display the first scatter plot
df.plot(kind='scatter', x='initial_cost', y='total_est_fee', rot=70)
plt.show()

# Create and display the second scatter plot
df_subset.plot(kind='scatter', x='initial_cost', y='total_est_fee', rot=70)
plt.show()
```

# Recognizing tidy data

For data to be tidy, it must have:

* Each variable as a separate column.
* Each row as a separate observation

As a data scientist, you'll encounter data that is represented in a variety of different ways, so it is important to be able to recognize tidy (or untidy) data when you see it

In this exercise, two example datasets have been pre-loaded into the DataFrames df1 and df2. Only one of them is tidy. Your job is to explore these further in the IPython Shell and identify the one that is not tidy, and why it is not tidy.

In the rest of this course, you will frequently be asked to explore the structure of DataFrames in the IPython Shell prior to performing different operations on them. Doing this will not only strengthen your comprehension of the data cleaning concepts covered in this course, but will also help you realize and take advantage of the relationship between working in the Shell and in the script.


# Reshaping your data using melt
Melting data is the process of turning columns of your data into rows of data. Consider the DataFrames from the previous exercise. In the tidy DataFrame, the variables Ozone, Solar.R, Wind, and Temp each had their own column. If, however, you wanted these variables to be in rows instead, you could melt the DataFrame. In doing so, however, you would make the data untidy! This is important to keep in mind: Depending on how your data is represented, you will have to reshape it differently.
In this exercise, you will practice melting a DataFrame using pd.melt(). There are two parameters you should be aware of: id_vars and value_vars. The id_vars represent the columns of the data you do not want to melt (i.e., keep it in its current shape), while the value_vars represent the columns you do wish to melt into rows. By default, if no value_vars are provided, all columns not set in the id_vars will be melted. This could save a bit of typing, depending on the number of columns that need to be melted


The (tidy) DataFrame airquality has been pre-loaded. Your job is to melt its Ozone, Solar.R, Wind, and Temp columns into rows. Later in this chapter, you'll learn how to bring this melted DataFrame back into a tidy form.

## Instructions
* Print the head of airquality.
* Use pd.melt() to melt the Ozone, Solar.R, Wind, and Temp columns of airquality into rows. Do this by using id_vars to specify the columns you do not wish to melt: 'Month' and 'Day'.
* Print the head of airquality_melt

```python

# Print the head of airquality
print(airquality.head())

# Melt airquality: airquality_melt
airquality_melt = pd.melt(airquality, id_vars=['Month', 'Day'])

# Print the head of airquality_melt
print(airquality_melt.head())
```
# Customizing melted data

When melting DataFrames, it would be better to have column names more meaningful than variable and value.
The default names may work in certain situations, but it's best to always have data that is self explanatory.
You can rename the variable column by specifying an argument to the var_name parameter, and the value column by specifying an argument to the value_name parameter. You will now practice doing exactly this. The DataFrame airquality has been pre-loaded for you.

## Instructions

* Print the head of airquality.
* Melt the Ozone, Solar.R, Wind, and Temp columns of airquality into rows, with the default variable column renamed to 'measurement' and * the default value column renamed to 'reading'. You can do this by specifying, respectively, the var_name and value_name parameters.
* Print the head of airquality_melt.

```python

# Print the head of airquality
print(airquality.head())

# Melt airquality: airquality_melt
airquality_melt = pd.melt(airquality, id_vars=['Month', 'Day'], var_name='measurement', value_name='reading')

# Print the head of airquality_melt
print(airquality_melt.head())
```
# Pivot data
Pivoting data is the opposite of melting it. Remember the tidy form that the airquality DataFrame was in before you melted it? You'll now begin pivoting it back into that form using the .pivot_table() method!
While melting takes a set of columns and turns it into a single column, pivoting will create a new column for each unique value in a specified column.
.pivot_table() has an index parameter which you can use to specify the columns that you don't want pivoted: It is similar to the id_vars parameter of pd.melt(). Two other parameters that you have to specify are columns (the name of the column you want to pivot), and values (the values to be used when the column is pivoted). The melted DataFrame airquality_melt has been pre-loaded for you.

## Instructions
* Print the head of airquality_melt.
* Pivot airquality_melt by using .pivot_table() with the rows indexed by 'Month' and 'Day', the columns indexed by 'measurement', and the values populated with 'reading'.
* Print the head of airquality_pivot.

```python

# Print the head of airquality_melt
print(airquality_melt.head())

# Pivot airquality_melt: airquality_pivot
airquality_pivot = airquality_melt.pivot_table(index=['Month', 'Day'], columns='measurement', values='reading')

# Print the head of airquality_pivot
print(airquality_pivot.head())
```
# Resetting the index of a DataFrame
After pivoting airquality_melt in the previous exercise, you didn't quite get back the original DataFrame.

What you got back instead was a pandas DataFrame with a hierarchical index (also known as a MultiIndex).
Hierarchical indexes are covered in depth in Manipulating DataFrames with pandas. In essence, they allow you to group columns or rows by another variable - in this case, by 'Month' as well as 'Day'. 

There's a very simple method you can use to get back the original DataFrame from the pivoted DataFrame: .reset_index(). Dan didn't show you how to use this method in the video, but you're now going to practice using it in this exercise to get back the original DataFrame from airquality_pivot, which has been pre-loaded.

## Instructions
* Print the index of airquality_pivot by accessing its .index attribute. This has been done for you.
* Reset the index of airquality_pivot using its .reset_index() method.
* Print the new index of airquality_pivot.
* Print the head of airquality_pivot.

```python

# Print the index of airquality_pivot
print(airquality_pivot.index)

# Reset the index of airquality_pivot: airquality_pivot_reset
airquality_pivot_reset = airquality_pivot.reset_index()

# Print the new index of airquality_pivot_reset
print(airquality_pivot_reset.index)

# Print the head of airquality_pivot_reset
print(airquality_pivot_reset.head())
```
# Pivoting duplicate values
So far, you've used the .pivot_table() method when there are multiple index values you want to hold constant during a pivot. In the video, Dan showed you how you can also use pivot tables to deal with duplicate values by providing an aggregation function through the aggfunc parameter. Here, you're going to combine both these uses of pivot tables.

Let's say your data collection method accidentally duplicated your dataset. Such a dataset, in which each row is duplicated, has been pre-loaded as airquality_dup. In addition, the airquality_melt DataFrame from the previous exercise has been pre-loaded. Explore their shapes in the IPython Shell by accessing their .shape attributes to confirm the duplicate rows present in airquality_dup.

You'll see that by using .pivot_table() and the aggfunc parameter, you can not only reshape your data, but also remove duplicates. Finally, you can then flatten the columns of the pivoted DataFrame using .reset_index().
NumPy and pandas have been imported as np and pd respectively.

## Instructions
* Pivot airquality_dup by using .pivot_table() with the rows indexed by 'Month' and 'Day', the columns indexed by 'measurement', and the values populated with 'reading'. Use np.mean for the aggregation function. 
* Flatten airquality_pivot by resetting its index.
* Print the head of airquality_pivot and then the original airquality DataFrame to compare their structure.

```python

# Pivot airquality_dup: airquality_pivot
airquality_pivot = airquality_dup.pivot_table (index=['Month', 'Day'], columns='measurement', values='reading', aggfunc=np.mean)

# Reset the index of airquality_pivot
airquality_pivot = airquality_pivot.reset_index()

# Print the head of airquality_pivot
print(airquality_pivot.head())

# Print the head of airquality
print(airquality.head())
```
# Splitting a column with .str
The dataset you saw in the video, consisting of case counts of tuberculosis by country, year, gender, and age group, has been pre-loaded into a DataFrame as tb.

In this exercise, you're going to tidy the 'm014' column, which represents males aged 0-14 years of age. In order to parse this value, you need to extract the first letter into a new column for gender, and the rest into a column for age_group. Here, since you can parse values by position, you can take advantage of pandas' vectorized string slicing by using the str attribute of columns of type object.

Begin by printing the columns of tb in the IPython Shell using its .columns attribute, and take note of the problematic column.
## Instructions
* Melt tb keeping 'country' and 'year' fixed.
* Create a 'gender' column by slicing the first letter of the variable column of tb_melt.
* Create an 'age_group' column by slicing the rest of the variable column of tb_melt.
* Print the head of tb_melt. This has been done for you, so hit 'Submit Answer' to see the results!

```python

# Melt tb: tb_melt
tb_melt = pd.melt(frame=df, id_vars=['country', 'year'])

# Create the 'gender' column
tb_melt['gender'] = tb_melt.variable.str[0]

# Create the 'age_group' column
tb_melt['age_group'] = tb_melt.variable.str[1:]

# Print the head of tb_melt
print(tb_melt.head())

```
# Splitting a column with .split() and .get()
Another common way multiple variables are stored in columns is with a delimiter. You'll learn how to deal with such cases in this exercise, using a dataset consisting of Ebola cases and death counts by state and country. It has been pre-loaded into a DataFrame as ebola.

Print the columns of ebola in the IPython Shell using ebola.columns. Notice that the data has column names such as Cases_Guinea and Deaths_Guinea. Here, the underscore _ serves as a delimiter between the first part (cases or deaths), and the second part (country).

This time, you cannot directly slice the variable by position as in the previous exercise. You now need to use Python's built-in string method called .split(). By default, this method will split a string into parts separated by a space. However, in this case you want it to split by an underscore. You can do this on Cases_Guinea, for example, using Cases_Guinea.split('_'), which returns the list ['Cases', 'Guinea'].

The next challenge is to extract the first element of this list and assign it to a type variable, and the second element of the list to a country variable. You can accomplish this by accessing the str attribute of the column and using the .get() method to retrieve the 0 or 1 index, depending on the part you want.

## Instructions
* Melt ebola using 'Date' and 'Day' as the id_vars, 'type_country' as the var_name, and 'counts' as the value_name.
* Create a column called 'str_split' by splitting the 'type_country' column of ebola_melt on '_'. Note that you will first have to access the str attribute of type_country before you can use .split().
* Create a column called 'type' by using the .get() method to retrieve index 0 of the 'str_split' column of ebola_melt.
* Create a column called 'country' by using the .get() method to retrieve index 1 of the 'str_split' column of ebola_melt.
* Print the head of ebola. This has been done for you, so hit 'Submit Answer' to view the results!

```python

# Melt ebola: ebola_melt
ebola_melt = pd.melt(ebola, id_vars=['Date', 'Day'], var_name='type_country', value_name='counts')

# Create the 'str_split' column
ebola_melt['str_split'] = ebola_melt.type_country.str.split('_')

# Create the 'type' column
ebola_melt['type'] = ebola_melt.str_split.str.get(0)

# Create the 'country' column
ebola_melt['country'] = ebola_melt.str_split.str.get(1)

# Print the head of ebola_melt
print(ebola_melt.head())
```
# Combining rows of data
The dataset you'll be working with here relates to NYC Uber data. The original dataset has all the originating Uber pickup locations by time and latitude and longitude. For didactic purposes, you'll be working with a very small portion of the actual data.
Three DataFrames have been pre-loaded: uber1, which contains data for April 2014, uber2, which contains data for May 2014, and uber3, which contains data for June 2014. Your job in this exercise is to concatenate these DataFrames together such that the resulting DataFrame has the data for all three months.
Begin by exploring the structure of these three DataFrames in the IPython Shell using methods such as .head().

## Instructions
* Concatenate uber1, uber2, and uber3 together using pd.concat(). You'll have to pass the DataFrames in as a list.
* Print the shape and then the head of the concatenated DataFrame, row_concat.

```python

# Concatenate uber1, uber2, and uber3: row_concat
row_concat = pd.concat([uber1, uber2, uber3])

# Print the shape of row_concat
print(row_concat.shape)

# Print the head of row_concat
print(row_concat.head())
```
# Combining columns of data
Think of column-wise concatenation of data as stitching data together from the sides instead of the top and bottom. To perform this action, you use the same pd.concat() function, but this time with the keyword argument axis=1. The default, axis=0, is for a row-wise concatenation.

You'll return to the Ebola dataset you worked with briefly in the last chapter. It has been pre-loaded into a DataFrame called ebola_melt. In this DataFrame, the status and country of a patient is contained in a single column. This column has been parsed into a new DataFrame, status_country, where there are separate columns for status and country. 

Explore the ebola_melt and status_country DataFrames in the IPython Shell. Your job is to concatenate them column-wise in order to obtain a final, clean DataFrame.

## Instructions

* Concatenate ebola_melt and status_country column-wise into a single DataFrame called ebola_tidy. Be sure to specify axis=1 and to pass the two DataFrames in as a list.

* Print the shape and then the head of the concatenated DataFrame, ebola_tidy.

```python

# Concatenate ebola_melt and status_country column-wise: ebola_tidy
ebola_tidy = pd.concat([ebola_melt,status_country],axis=1)

# Print the shape of ebola_tidy
print(ebola_tidy.shape)

# Print the head of ebola_tidy
print(ebola_tidy.head())
```
# Finding files that match a pattern
You're now going to practice using the glob module to find all csv files in the workspace. In the next exercise, you'll programmatically load them into DataFrames.

As Dan showed you in the video, the glob module has a function called glob that takes a pattern and returns a list of the files in the working directory that match that pattern.

For example, if you know the pattern is part_ single digit number .csv, you can write the pattern as 'part_?.csv' (which would match part_1.csv, part_2.csv, part_3.csv, etc.)

Similarly, you can find all .csv files with '*.csv', or all parts with 'part_*'. The ? wildcard represents any 1 character, and the * wildcard represents any number of characters.

## Instructions
* Import the glob module along with pandas (as its usual alias pd).
* Write a pattern to match all .csv files.
* Save all files that match the pattern using the glob() function within the glob module. That is, by using glob.glob().
* Print the list of file names. This has been done for you.
* Read the second file in csv_files (i.e., index 1) into a DataFrame called csv2.
* Hit 'Submit Answer' to print the head of csv2. Does it look familiar?

```python

# Import necessary modules
import pandas as pd
import glob

# Write the pattern: pattern
pattern = '*.csv'

# Save all file matches: csv_files
csv_files = glob.glob(pattern)

# Print the file names
print(csv_files)

# Load the second file into a DataFrame: csv2
csv2 = pd.read_csv(csv_files[1])

# Print the head of csv2
print(csv2.head())
```
# Iterating and concatenating all matches
Now that you have a list of filenames to load, you can load all the files into a list of DataFrames that can then be concatenated.
You'll start with an empty list called frames. Your job is to use a for loop to iterate through each of the filenames, read each filename into a DataFrame, and then append it to the frames list.

You can then concatenate this list of DataFrames using pd.concat(). Go for it!
## Instructions
* Write a for loop to iterate through csv_files:
* In each iteration of the loop, read csv into a DataFrame called df.
* After creating df, append it to the list frames using the .append() method.
* Concatenate frames into a single DataFrame called uber.
* Hit 'Submit Answer' to see the head and shape of the concatenated DataFrame!

```python

# Create an empty list: frames
frames = []

#  Iterate over csv_files
for csv in csv_files:

    #  Read csv into a DataFrame: df
    df = pd.read_csv(csv)
    
    # Append df to frames
    frames.append(df)

# Concatenate frames into a single DataFrame: uber
uber = pd.concat(frames)

# Print the shape of uber
print(uber.shape)

# Print the head of uber
print(uber.head())
```
# 1-to-1 data merge

Merging data allows you to combine disparate datasets into a single dataset to do more complex analysis.
Here, you'll be using survey data that contains readings that William Dyer, Frank Pabodie, and Valentina Roerich took in the late 1920 and 1930 while they were on an expedition towards Antarctica. The dataset was taken from a sqlite database from the Software Carpentry SQL lesson. 

Two DataFrames have been pre-loaded: site and visited. Explore them in the IPython Shell and take note of their structure and column names. Your task is to perform a 1-to-1 merge of these two DataFrames using the 'name' column of site and the 'site' column of visited.

## Instructions
* Merge the site and visited DataFrames on the 'name' column of site and 'site' column of visited.
* Print the merged DataFrame o2o.

```python

# Merge the DataFrames: o2o
o2o = pd.merge(left= site, right= visited , left_on='name', right_on='site')
# Print o2o
print(o2o)
```
# Many-to-1 data merge
In a many-to-one (or one-to-many) merge, one of the values will be duplicated and recycled in the output. That is, one of the keys in the merge is not unique

Here, the two DataFrames site and visited have been pre-loaded once again. Note that this time, visited has multiple entries for the site column. Confirm this by exploring it in the IPython Shell.
The .merge() method call is the same as the 1-to-1 merge from the previous exercise, but the data and output will be different.

## Instructions
* Merge the site and visited DataFrames on the 'name' column of site and 'site' column of visited, exactly as you did in the previous exercise.
* Print the merged DataFrame and then hit 'Submit Answer' to see the different output produced by this merge!

```python

# Merge the DataFrames: m2o
m2o = pd.merge(left= site, right= visited , left_on='name', right_on='site')
# Print m2o
print(m2o)
```
# Many-to-many data merge
The final merging scenario occurs when both DataFrames do not have unique keys for a merge. What happens here is that for each duplicated key, every pairwise combination will be created.

Two example DataFrames that share common key values have been pre-loaded: df1 and df2. Another DataFrame df3, which is the result of df1 merged with df2, has been pre-loaded. All three DataFrames have been printed - look at the output and notice how pairwise combinations have been created. This example is to help you develop your intuition for many-to-many merges.
Here, you'll work with the site and visited DataFrames from before, and a new survey DataFrame. Your task is to merge site and visited as you did in the earlier exercises. You will then merge this merged DataFrame with survey.
Begin by exploring the site, visited, and survey DataFrames in the IPython Shell.

## Instructions

* Merge the site and visited DataFrames on the 'name' column of site and 'site' column of visited, exactly as you did in the previous two exercises. Save the result as m2m.
* Merge the m2m and survey DataFrames on the 'ident' column of m2m and 'taken' column of survey.
* Hit 'Submit Answer' to print the first 20 lines of the merged DataFrame!

```python

# Merge site and visited: m2m
m2m = pd.merge(left= site, right= visited, left_on= 'name', right_on= 'site')

# Merge m2m and survey: m2m
m2m = pd.merge(left= m2m, right= survey, left_on= 'ident', right_on= 'taken')

# Print the first 20 lines of m2m
print(m2m.head(20))
```
# Converting data types
In this exercise, you'll see how ensuring all categorical variables in a DataFrame are of type category reduces memory usage.
The tips dataset has been loaded into a DataFrame called tips. This data contains information about how much a customer tipped, whether the customer was male or female, a smoker or not, etc. 

Look at the output of tips.info() in the IPython Shell. You'll note that two columns that should be categorical - sex and smoker - are instead of type object, which is pandas' way of storing arbitrary strings. Your job is to convert these two columns to type category and note the reduced memory usage.

## Instructions
* Convert the sex column of the tips DataFrame to type 'category' using the .astype() method.
* Convert the smoker column of the tips DataFrame.
* Print the memory usage of tips after converting the data types of the columns. Use the .info() method to do this

```python

# Convert the sex column to type 'category'
tips.sex = tips.sex.astype('category')

# Convert the smoker column to type 'category'
tips.smoker = tips.smoker.astype('category')

# Print the info of tips
print(tips.info())
```
# Working with numeric data
If you expect the data type of a column to be numeric (int or float), but instead it is of type object, this typically means that there is a non numeric value in the column, which also signifies bad data.

You can use the pd.to_numeric() function to convert a column into a numeric data type. If the function raises an error, you can be sure that there is a bad value within the column. You can either use the techniques you learned in Chapter 1 to do some exploratory data analysis and find the bad value, or you can choose to ignore or coerce the value into a missing value, NaN.

A modified version of the tips dataset has been pre-loaded into a DataFrame called tips. For instructional purposes, it has been pre-processed to introduce some 'bad' data for you to clean. Use the .info() method to explore this. You'll note that the total_bill and tip columns, which should be numeric, are instead of type object. Your job is to fix this.

## Instructions
* Use pd.to_numeric() to convert the 'total_bill' column of tips to a numeric data type. Coerce the errors to NaN by specifying the keyword argument errors='coerce'.
* Convert the 'tip' column of 'tips' to a numeric data type exactly as you did for the 'total_bill' column.
* Print the info of tips to confirm that the data types of 'total_bill' and 'tips' are numeric.

```python

# Convert 'total_bill' to a numeric dtype
tips['total_bill'] = pd.to_numeric(tips['total_bill'], errors= 'coerce')

# Convert 'tip' to a numeric dtype
tips['tip'] = pd.to_numeric(tips['tip'],errors= 'coerce')

# Print the info of tips
print(tips.info())
```
# String parsing with regular expressions
In the video, Dan introduced you to the basics of regular expressions, which are powerful ways of defining patterns to match strings. This exercise will get you started with writing them.

When working with data, it is sometimes necessary to write a regular expression to look for properly entered values. Phone numbers in a dataset is a common field that needs to be checked for validity. Your job in this exercise is to define a regular expression to match US phone numbers that fit the pattern of xxx-xxx-xxxx.

The regular expression module in python is re. When performing pattern matching on data, since the pattern will be used for a match across multiple rows, it's better to compile the pattern first using re.compile(), and then use the compiled pattern to match values.

## Instructions
* Import re.
* Compile a pattern that matches a phone number of the format xxx-xxx-xxxx.
* Use \d{x} to match x digits. Here you'll need to use it three times: twice to match 3 digits, and once to match 4 digits.
* Place the regular expression inside re.compile().
* Using the .match() method on prog, check whether the pattern matches the string '123-456-7890'.
* Using the same approach, now check whether the pattern matches the string '1123-456-7890'.

```python

# Import the regular expression module
import re

# Compile the pattern: prog
prog = re.compile('\d{3}-\d{3}-\d{4}')

# See if the pattern matches
result = prog.match('123-456-7890')
print(bool(result))

# See if the pattern matches
result2 = prog.match('1123-456-7890')
print(bool(result2))
```
# Extracting numerical values from strings
Extracting numbers from strings is a common task, particularly when working with unstructured data or log files.

Say you have the following string: 
```code 

'the recipe calls for 6 strawberries and 2 bananas'
```
It would be useful to extract the 6 and the 2 from this string to be saved for later use when comparing strawberry to banana ratios.
When using a regular expression to extract multiple numbers (or multiple pattern matches, to be exact), you can use the re.findall() function. Dan did not discuss this in the video, but it is straightforward to use: You pass in a pattern and a string to re.findall(), and it will return a list of the matches.

## Instructions
* Import re.
* Write a pattern that will find all the numbers in the following string: 'the recipe calls for 10 strawberries and 1 banana'. To do this:
* Use the re.findall() function and pass it two arguments: the pattern, followed by the string.
* \d is the pattern required to find digits. This should be followed with a + so that the previous element is matched one or more times. * This ensures that 10 is viewed as one number and not as 1 and 0.
* Print the matches to confirm that your regular expression found the values 10 and 1.

```python

# Import the regular expression module
import re

# Find the numeric values: matches
matches = re.findall('\d+','the recipe calls for 10 strawberries and 1 bananas')

# Print the matches
print(matches)
```
# Pattern matching
In this exercise, you'll continue practicing your regular expression skills. For each provided string, your job is to write the appropriate pattern to match it.

## Instructions
* Write patterns to match:
* A telephone number of the format xxx-xxx-xxxx. You already did this in a previous exercise.
* A string of the format: A dollar sign, an arbitrary number of digits, a decimal point, 2 digits.
* Use \$ to match the dollar sign, \d* to match an arbitrary number of digits, \. to match the decimal point, and \d{x} to match x number of digits.
* A capital letter, followed by an arbitrary number of alphanumeric characters.
* Use [A-Z] to match any capital letter followed by \w* to match an arbitrary number of alphanumeric characters.

```python

# Write the first pattern
pattern1 = bool(re.match(pattern='\d{3}-\d{3}-\d{4}', string='123-456-7890'))
print(pattern1)

# Write the second pattern
pattern2 = bool(re.match(pattern='\$\d*\.\d{2}', string='$123.45'))
print(pattern2)

# Write the third pattern
# [A-Z] =  pattern \w*
pattern3 = bool(re.match(pattern='\w*', string='Australia'))
print(pattern3)
```
# Custom functions to clean data
You'll now practice writing functions to clean data. 

The tips dataset has been pre-loaded into a DataFrame called tips. It has a 'sex' column that contains the values 'Male' or 'Female'. Your job is to write a function that will recode ``` Male ``` to 1, ``` Female ``` to 0, and return np.nan for all entries of 'sex' that are neither 'Male' nor 'Female'. 

Recoding variables like this is a common data cleaning task. Functions provide a mechanism for you to abstract away complex bits of code as well as reuse code. This makes your code more readable and less error prone.
As Dan showed you in the videos, you can use the .apply() method to apply a function across entire rows or columns of DataFrames. However, note that each column of a DataFrame is a pandas Series. Functions can also be applied across Series. Here, you will apply your function over the 'sex' column.

## Instructions
* Define a function named recode_sex() that has one parameter: sex_value.
* If sex_value equals 'Male', return 1.
* Else, if sex_value equals 'Female', return 0.
* If sex_value does not equal 'Male' or 'Female', return np.nan. NumPy has been pre-imported for you.
* Apply your recode_sex() function over tips.sex using the .apply() method to create a new column: 'sex_recode'. Note that when passing in a function inside the .apply() method, you don't need to specify the parentheses after the function name.
* Hit 'Submit Answer' and take note of the new 'sex_recode' column in the tips DataFrame!

```python

# Define recode_sex()
def recode_sex(sex_value):

    # Return 1 if sex_value is 'Male'
    if sex_value == 'Male':
        return 1
    
    # Return 0 if sex_value is 'Female'
    elif sex_value == 'Female':
        return 0
        
    # Return np.nan    
    else:
        return np.nan

# Apply the function to the sex column
tips['sex_recode'] = tips.sex.apply(recode_sex)

# Print the first five rows of tips
print(tips.head())
```
# Lambda functions
You'll now be introduced to a powerful Python feature that will help you clean your data more effectively: lambda functions. Instead of using the def syntax that you used in the previous exercise, lambda functions let you make simple, one-line functions. 

For example, here's a function that squares a variable used in an .apply() method:

```pyhton

def my_square(x):
    return x ** 2

df.apply(my_square)
```
The equivalent code using a lambda function is:
```code 

df.apply(lambda x: x ** 2)
```
The lambda function takes one parameter - the variable x. The function itself just squares x and returns the result, which is whatever the one line of code evaluates to. In this way, lambda functions can make your code concise and Pythonic.
The tips dataset has been pre-loaded into a DataFrame called tips. Your job is to clean its 'total_dollar' column by removing the dollar sign. You'll do this using two different methods: With the .replace() method, and with regular expressions. The regular expression module re has been pre-imported.

## Instructions
* Use the .replace() method inside a lambda function to remove the dollar sign from the 'total_dollar' column of tips.
* You need to specify two arguments to the .replace() method: The string to be replaced ('$'), and the string to replace it by ('').
* Apply the lambda function over the 'total_dollar' column of tips.
* Use a regular expression to remove the dollar sign from the 'total_dollar' column of tips.
* The pattern has been provided for you: It is the first argument of the re.findall() function.
* Complete the rest of the lambda function and apply it over the 'total_dollar' column of tips. Notice that because re.findall() returns a list, you have to slice it in order to access the actual value.
* Hit 'Submit Answer' to verify that you have removed the dollar sign from the column.

```python

# Write the lambda function using replace
tips['total_dollar_replace'] = tips.total_dollar.apply(lambda x: x.replace('$', ''))

# Write the lambda function using regular expressions
tips['total_dollar_re'] = tips.total_dollar.apply(lambda x: re.findall('\d+\.\d+', x)[0])

# Print the head of tips
print(tips.head())
```
# Dropping duplicate data
Duplicate data causes a variety of problems. From the point of view of performance, they use up unnecessary amounts of memory and cause unneeded calculations to be performed when processing data. In addition, they can also bias any analysis results.

A dataset consisting of the performance of songs on the Billboard charts has been pre-loaded into a DataFrame called billboard. Check out its columns in the IPython Shell. Your job in this exercise is to subset this DataFrame and then drop all duplicate rows.

## Instructions
* Create a new DataFrame called tracks that contains the following columns from billboard: 'year', 'artist', 'track', and 'time'.
* Print the info of tracks. This has been done for you.
* Drop duplicate rows from tracks using the .drop_duplicates() method. Save the result to tracks_no_duplicates.
* Print the info of tracks_no_duplicates. This has been done for you, so hit 'Submit Answer' to see the results!

```python

# Create the new DataFrame: tracks
tracks = billboard[['year','artist','track','time']]

# Print info of tracks
print(tracks.info())

# Drop the duplicates: tracks_no_duplicates
tracks_no_duplicates = tracks.drop_duplicates()

# Print info of tracks
print(tracks_no_duplicates.info())
```





































































