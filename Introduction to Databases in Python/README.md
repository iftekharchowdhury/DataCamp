# Engines and Connection Strings
Alright, it's time to create your first engine! An engine is just a common interface to a database, and the information it requires to connect to one is contained in a connection string, such as sqlite:///census_nyc.sqlite. Here, sqlite is the database driver, while census_nyc.sqlite is a SQLite file contained in the local directory.
You can learn a lot more about connection strings in the SQLAlchemy documentation.
Your job in this exercise is to create an engine that connects to a local SQLite file named census.sqlite. 
Then, print the names of the tables it contains using the .table_names() method. Note that when you just want to print the table names, you do not need to use engine.connect() after creating the engine.

## Instructions
Import create_engine from the sqlalchemy module.
Using the create_engine() function, create an engine for a local file named census.sqlite with sqlite as the driver. Be sure to enclose the connection string within quotation marks.
Print the output from the .table_names() method on the engine.

```python

# Import create_engine
from sqlalchemy import create_engine

# Create an engine that connects to the census.sqlite file: engine
engine = create_engine("sqlite:///census.sqlite")

# Print table names
print(engine.table_names())
```
# Autoloading Tables from a Database
SQLAlchemy can be used to automatically load tables from a database using something called reflection. Reflection is the process of reading the database and building the metadata based on that information. It's the opposite of creating a Table by hand and is very useful for working with existing databases. To perform reflection, you need to import the Table object from the SQLAlchemy package. Then, you use this Table object to read your table from the engine and autoload the columns. Using the Table object in this manner is a lot like passing arguments to a function. For example, to autoload the columns with the engine, you have to specify the keyword arguments autoload=True and autoload_with=engine to Table().
In this exercise, your job is to reflect the census table available on your engine into a variable called census. The metadata has already been loaded for you using MetaData() and is available in the variable metadata

## Instructions
Import the Table object from sqlalchemy.
Reflect the census table by using the Table object with the arguments: 
The name of the table as a string ('census').
The metadata, contained in the variable metadata.
autoload=True
The engine to autoload with - in this case, engine.
Print the details of census using the repr() function.

```python

# Import Table
from sqlalchemy import Table

# Reflect census table from the engine: census
census = Table('census', metadata, autoload=True, autoload_with=engine)

# Print census table metadata
print(repr(census))
```
# Viewing Table Details
Great job reflecting the census table! Now you can begin to learn more about the columns and structure of your table. It is important to get an understanding of your database by examining the column names. This can be done by using the .columns attribute and accessing the .keys() method. For example, census.columns.keys() would return a list of column names of the census table.
Following this, we can use the metadata container to find out more details about the reflected table such as the columns and their types. For example, table objects are stored in the metadata.tables dictionary, so you can get the metadata of your census table with metadata.tables['census']. This is similar to your use of the repr() function on the census table from the previous exercise.


```python

# Reflect the census table from the engine: census
census = Table('census', metadata, autoload=True, autoload_with=engine)

# Print the column names
print(census.columns.keys())

# Print full table metadata
print(repr(metadata.tables['census']))
```

# Selecting data from a Table: raw SQL
Using what we just learned about SQL and applying the .execute() method on our connection, we can leverage a raw SQL query to query all the records in our census table. The object returned by the .execute() method is a ResultProxy. On this ResultProxy, we can then use the .fetchall() method to get our results - that is, the ResultSet.
In this exercise, you'll use a traditional SQL query. In the next exercise, you'll move to SQLAlchemy and begin to understand its advantages. Go for it!

## Instructions
Build a SQL statement to query all the columns from census and store it in stmt. Note that your SQL statement must be a string.
Use the .execute() and .fetchall() methods on connection and store the result in results. Remember that .execute() comes before .fetchall() and that stmt needs to be passed to .execute().
Print results.

```python

# Build select statement for census table: stmt
stmt = "select * from census"

# Execute the statement and fetch the results: results
results = connection.execute(stmt).fetchall()

# Print results
print(results)
```

# Selecting data from a Table with SQLAlchemy
Excellent work so far! It's now time to build your first select statement using SQLAlchemy. SQLAlchemy provides a nice "Pythonic" way of interacting with databases. So rather than dealing with the differences between specific dialects of traditional SQL such as MySQL or PostgreSQL, you can leverage the Pythonic framework of SQLAlchemy to streamline your workflow and more efficiently query your data. For this reason, it is worth learning even if you may already be familiar with traditional SQL.
In this exercise, you'll once again build a statement to query all records from the census table. This time, however, you'll make use of the select() function of the sqlalchemy module. This function requires a list of tables or columns as the only required argument.
Table and MetaData have already been imported. The metadata is available as metadata and the connection to the database as connection.

## Instructions
* Import select from the sqlalchemy module.
* Reflect the census table. This code is already written for you.
* Create a query using the select() function to retrieve the census table. To do so, pass a list to select() containing a single element: census.
* Print stmt to see the actual SQL query being created. This code has been written for you.
* Using the provided print() function, print all the records from the census table. To do this:
* Use the .execute() method on connection with stmt as the argument to retrieve the ResultProxy.
* Use .fetchall() on connection.execute(stmt) to retrieve the ResultSet.

 ```python
 
 # Import select
from sqlalchemy import select

# Reflect census table via engine: census
census = Table('census', metadata, autoload=True, autoload_with=engine)

# Build select statement for census table: stmt
stmt = select([census])

# Print the emitted statement to see the SQL emitted
print(stmt)

# Execute the statement and print the results
print(connection.execute(stmt).fetchall())
 ```

# Handling a ResultSet

Recall the differences between a ResultProxy and a ResultSet:
ResultProxy: The object returned by the .execute() method. It can be used in a variety of ways to get the data returned by the query.
ResultSet: The actual data asked for in the query when using a fetch method such as .fetchall() on a ResultProxy.
This separation between the ResultSet and ResultProxy allows us to fetch as much or as little data as we desire.

Once we have a ResultSet, we can use Python to access all the data within it by column name and by list style indexes. For example, you can get the first row of the results by using results[0]. With that first row then assigned to a variable first_row, you can get data from the first column by either using first_row[0] or by column name such as first_row['column_name']. You'll now practice exactly this using the ResultSet you obtained from the census table in the previous exercise. It is stored in the variable results. Enjoy!

## Instructions
* Extract the first row of results and assign it to the variable first_row.
* Print the value of the first column in first_row.
* Print the value of the 'state' column in first_row.

```python

# Get the first row of the results by using an index: first_row
first_row = results[0]

# Print the first row of the results
print(first_row)

# Print the first column of the first row by using an index
print(first_row[0])

# Print the 'state' column of the first row by using its name
print(first_row['state'])
```
# Connecting to a PostgreSQL Database
In these exercises, you will be working with real databases hosted on the cloud via Amazon Web Services (AWS)! 
Let's begin by connecting to a PostgreSQL database. When connecting to a PostgreSQL database, many prefer to use the psycopg2 database driver as it supports practically all of PostgreSQL's features efficiently and is the standard dialect for PostgreSQL in SQLAlchemy.
You might recall from Chapter 1 that we use the create_engine() function and a connection string to connect to a database. 

There are three components to the connection string in this exercise: the dialect and driver ('postgresql+psycopg2://'), followed by the username and password ('student:datacamp'), followed by the host and port ('@postgresql.csrrinzqubik.us-east-1.rds.amazonaws.com:5432/'), and finally, the database name ('census'). You will have to pass this string as an argument to create_engine() in order to connect to the database.

## Instructions
* Import create_engine from sqlalchemy.
* Create an engine to the census database by concatenating the following strings:
'postgresql+psycopg2://'
'student:datacamp'
'@postgresql.csrrinzqubik.us-east-1.rds.amazonaws.com'
':5432/census'
* Use the .table_names() method on engine to print the table names.

```python

# Import create_engine function
from sqlalchemy import create_engine

# Create an engine to the census database
engine = create_engine('postgresql+psycopg2://student:datacamp'+'@postgresql.csrrinzqubik.us-east-1.rds.amazonaws.com:5432/census')

# Use the .table_names() method on the engine to print the table names
print(engine.table_names())
```
# Filter data selected from a Table - Simple

Having connected to the database, it's now time to practice filtering your queries!
As mentioned in the video, a where() clause is used to filter the data that a statement returns. For example, to select all the records from the census table where the sex is Female (or 'F') we would do the following:
select([census]).where(census.columns.sex == 'F')
In addition to == we can use basically any python comparison operator (such as <=, !=, etc) in the where() clause.

## Instructions
* Select all records from the census table by passing in census as a list to select().
* Append a where clause to stmt to return only the records with a state of 'New York'.
* Execute the statement stmt using .execute() and retrieve the results using .fetchall().
* Iterate over results and print the age, sex and pop2008 columns from each record. For example, you can print out the age of result with result.age.

```python

# Create a select query: stmt
stmt = select([census])

# Add a where clause to filter the results to only those for New York
stmt = stmt.where(census.columns.state == 'New York')

# Execute the query to retrieve all the data returned: results
results = connection.execute(stmt).fetchall()
print (results)
# Loop over the results and print the age, sex, and pop2008
for result in results:
    print(result.age, result.sex, result.pop2008)
```
# Filter data selected from a Table - Expressions
In addition to standard Python comparators, we can also use methods such as in_() to create more powerful where() clauses. You can see a full list of expressions in the SQLAlchemy Documentation.
We've already created a list of some of the most densely populated states.

## Instructions
* Select all records from the census table by passing it in as a list to select().
* Append a where clause to return all the records with a state in the states list. Use in_(states) on census.columns.state to do this.
* Loop over the ResultProxy connection.execute(stmt) and print the state and pop2000 columns from each record.

```python

# Create a query for the census table: stmt
stmt = select([census])

# Append a where clause to match all the states in_ the list states
stmt = stmt.where(census.columns.state.in_(states))

# Loop over the ResultProxy and print the state and its population in 2000
for ResultProxy in connection.execute(stmt):
    print(ResultProxy.state, ResultProxy.pop2000)
```
# Filter data selected from a Table - Advanced
You're really getting the hang of this! SQLAlchemy also allows users to use conjunctions such as and_(), or_(), and not_() to build more complex filtering. For example, we can get a set of records for people in New York who are 21 or 37 years old with the following code
```
stmt([census]).where(
  and_(census.columns.state == 'New York',
       or_(census.columns.age == 21,
          census.columns.age == 37
         )
      )
  )
```
## Instructions
* Import and_ from the sqlalchemy module.
* Select all records from the census table.
* Append a where clause to filter all the records whose state is 'California', and whose sex is not 'M'.
* Iterate over the ResultProxy and print the age and sex columns from each record.

```python

# Import and_
from sqlalchemy import and_

# Build a query for the census table: stmt
stmt = select([census])

# Append a where clause to select only non-male records from California using and_
stmt = stmt.where(
    # The state of California with a non-male sex
    and_(census.columns.state == 'California',
         census.columns.sex != 'M'
         )
)

# Loop over the ResultProxy printing the age and sex
for result in connection.execute(stmt):
    print(result.age, result.sex)
```

# Ordering by a Single Column
To sort the result output by a field, we use the .order_by() method. By default, the .order_by() method sorts from lowest to highest on the supplied column. You just have to pass in the name of the column you want sorted to .order_by(). In the video, for example, Jason used stmt.order_by(census.columns.state) to sort the result output by the state column.

## Instructions
* Select all records of the state column from the census table. To do this, pass census.columns.state as a list to select().
* Append an .order_by() to sort the result output by the state column.
* Execute stmt using the .execute() method on connection and retrieve all the results using .fetchall().
* Print the first 10 rows of results

```python

# Build a query to select the state column: stmt
stmt = select([census.columns.state])

# Order stmt by the state column
stmt = stmt.order_by(census.columns.state)

# Execute the query and store the results: results
results = connection.execute(stmt).fetchall()

# Print the first 10 results
print(results[:10])

```

# Ordering in Descending Order by a Single Column
You can also use .order_by() to sort from highest to lowest by wrapping a column in the desc() function. Although you haven't seen this function in action, it generalizes what you have already learned.
Pass desc() (for "descending") inside an .order_by() with the name of the column you want to sort by. For instance, stmt.order_by(desc(table.columns.column_name)) sorts column_name in descending order.

## Instructions
* Import desc from the sqlalchemy module.
* Select all records of the state column from the census table. 
* Append an .order_by() to sort the result output by the state column in descending order. Save the result as rev_stmt.
* Execute rev_stmt using connection.execute() and fetch all the results with .fetchall(). Save them as rev_results.
* Print the first 10 rows of rev_results.

```python

# Import desc
from sqlalchemy import desc

# Build a query to select the state column: stmt
stmt = select([census.columns.state])

# Order stmt by state in descending order: rev_stmt
rev_stmt = stmt.order_by(desc(census.columns.state))

# Execute the query and store the results: rev_results
rev_results = connection.execute(rev_stmt).fetchall()

# Print the first 10 rev_results
print(rev_results[:10])
```
# Ordering by Multiple Columns
We can pass multiple arguments to the .order_by() method to order by multiple columns. In fact, we can also sort in ascending or descending order for each individual column. Each column in the .order_by() method is fully sorted from left to right. This means that the first column is completely sorted, and then within each matching group of values in the first column, it's sorted by the next column in the .order_by() method. This process is repeated until all the columns in the .order_by() are sorted.

## instructions
Select all records of the state and age columns from the census table. 
Use .order_by() to sort the output of the state column in ascending order and age in descending order. (NOTE: desc is already imported).
Execute stmt using the .execute() method on connection and retrieve all the results using .fetchall().
Print the first 20 results.

```python

# Build a query to select state and age: stmt
stmt = select([census.columns.state, census.columns.age])

# Append order by to ascend by state and descend by age
stmt = stmt.order_by(census.columns.state, desc(census.columns.age))

# Execute the statement and store all the records: results
results = connection.execute(stmt).fetchall()

# Print the first 20 results
print(results[:20])
```
# Counting Distinct Data
As mentioned in the video, SQLAlchemy's func module provides access to built-in SQL functions that can make operations like counting and summing faster and more efficient. 
In the video, Jason used func.sum() to get a sum of the pop2008 column of census as shown below: 
select([func.sum(census.columns.pop2008)])
If instead you want to count the number of values in pop2008, you could use func.count() like this:
select([func.count(census.columns.pop2008)])
Furthermore, if you only want to count the distinct values of pop2008, you can use the .distinct() method:
select([func.count(census.columns.pop2008.distinct())])
In this exercise, you will practice using func.count() and .distinct() to get a count of the distinct number of states in census.
So far, you've seen .fetchall() and .first() used on a ResultProxy to get the results. The ResultProxy also has a method called .scalar() for getting just the value of a query that returns only one row and column. 
This can be very useful when you are querying for just a count or sum.

```python

# Build a query to count the distinct states values: stmt
stmt = select([func.count(census.columns.state.distinct())])

# Execute the query and store the scalar result: distinct_state_count
distinct_state_count = connection.execute(stmt).scalar()

# Print the distinct_state_count
print(distinct_state_count)
```

# Count of Records by State
Often, we want to get a count for each record with a particular value in another column. The .group_by() method helps answer this type of query. You can pass a column to the .group_by() method and use in an aggregate function like sum() or count(). Much like the .order_by() method, .group_by() can take multiple columns as arguments.

## instructions

* Import func from sqlalchemy.
* Build a select statement to get the value of the state field and a count of the values in the age field, and store it as stmt.
* Use the .group_by() method to group the statement by the state column.
* Execute stmt using the connection to get the count and store the results as results.
* Print the keys/column names of the results returned using results[0].keys()

```python

# Import func
from sqlalchemy import func

# Build a query to select the state and count of ages by state: stmt
stmt = select([census.columns.state, func.count(census.columns.age)])

# Group stmt by state
stmt = stmt.group_by(census.columns.state)

# Execute the statement and store all the records: results
results = connection.execute(stmt).fetchall()

# Print results
print(results)

# Print the keys/column names of the results returned
print(results[0].keys())
```
# Determining the Population Sum by State
To avoid confusion with query result column names like count_1, we can use the .label() method to provide a name for the resulting column. This gets appended to the function method we are using, and its argument is the name we want to use.
We can pair func.sum() with .group_by() to get a sum of the population by State and use the label() method to name the output.
We can also create the func.sum() expression before using it in the select statement. We do it the same way we would inside the select statement and store it in a variable. Then we use that variable in the select statement where the func.sum() would normally be.

## instructions
* Import func from sqlalchemy.
* Build an expression to calculate the sum of the values in the pop2008 field labeled as 'population'.
* Build a select statement to get the value of the state field and the sum of the values in pop2008.
* Group the statement by state using a .group_by() method.
* Execute stmt using the connection to get the count and store the results as results.
* Print the keys/column names of the results returned using results[0].keys().

```python

# Import func
from sqlalchemy import func

# Build an expression to calculate the sum of pop2008 labeled as population
pop2008_sum = func.sum(census.columns.pop2008).label('population')

# Build a query to select the state and sum of pop2008: stmt
stmt = select([census.columns.state, pop2008_sum])

# Group stmt by state
stmt = stmt.group_by(census.columns.state)

# Execute the statement and store all the records: results
results = connection.execute(stmt).fetchall()

# Print results
print(results)

# Print the keys/column names of the results returned
print(results[0].keys())
```

# SQLAlchemy ResultsProxy and Pandas Dataframes
We can feed a ResultProxy directly into a pandas DataFrame, which is the workhorse of many Data Scientists in PythonLand. Jason demonstrated this in the video. In this exercise, you'll follow exactly the same approach to convert a ResultProxy into a DataFrame.

## instructions
* Import pandas as pd.
* Create a DataFrame df using pd.DataFrame() on the ResultProxy results.
* Set the columns of the DataFrame df.columns to be the columns from the first result object results[0].keys().
* Print the DataFrame.

```python

# import pandas
import pandas as pd

# Create a DataFrame from the results: df
df = pd.DataFrame(results)

# Set column names
df.columns = results[0].keys()

# Print the Dataframe
print(df)
```
# From SQLAlchemy results to a Graph
We can also take advantage of pandas and Matplotlib to build figures of our data. Remember that data visualization is essential for both exploratory data analysis and communication of your data!

## Instructions
* Import matplotlib.pyplot as plt.
* Create a DataFrame df using pd.DataFrame() on the provided results.
* Set the columns of the DataFrame df.columns to be the columns from the first result object results[0].keys().
* Print the DataFrame df.
* Use the plot.bar() method on df to create a bar plot of the results.
* Display the plot with plt.show().

```python

# Import Pyplot as plt from matplotlib
import matplotlib.pyplot as plt

# Create a DataFrame from the results: df
df = pd.DataFrame(results)

# Set Column names
df.columns = results[0].keys()

# Print the DataFrame
print (df)

# Plot the DataFrame
df.plot.bar()
plt.show()
```

# Connecting to a MySQL Database
Before you jump into the calculation exercises, let's begin by connecting to our database. Recall that in the last chapter you connected to a PostgreSQL database. Now, you'll connect to a MySQL database, for which many prefer to use the pymysql database driver, which, like psycopg2 for PostgreSQL, you have to install prior to use. 

This connection string is going to start with 'mysql+pymysql://', indicating which dialect and driver you're using to establish the connection. The dialect block is followed by the 'username:password' combo. Next, you specify the host and port with the following '@host:port/'. Finally, you wrap up the connection string with the 'database_name'. 

Now you'll practice connecting to a MySQL database: it will be the same census database that you have already been working with. One of the great things about SQLAlchemy is that, after connecting, it abstracts over the type of database it has connected to and you can write the same SQLAlchemy code, regardless!

## Instructions
* Import the create_engine function from the sqlalchemy library.
* Create an engine to the census database by concatenating the following strings and passing them to create_engine():
* 'mysql+pymysql://' (the dialect and driver).
* 'student:datacamp' (the username and password).
* '@courses.csrrinzqubik.us-east-1.rds.amazonaws.com:3306/' (the host and port).
* 'census' (the database name).
* Use the .table_names() method on engine to print the table names.

```python

# Import create_engine function
from sqlalchemy import create_engine

# Create an engine to the census database
engine = create_engine('mysql+pymysql://'+'student:datacamp'+'@courses.csrrinzqubik.us-east-1.rds.amazonaws.com:3306/'+ 'census')

# Print the table names
print(engine.table_names())
```

# Calculating a Difference between Two Columns
Often, you'll need to perform math operations as part of a query, such as if you wanted to calculate the change in population from 2000 to 2008. For math operations on numbers, the operators in SQLAlchemy work the same way as they do in Python.
You can use these operators to perform addition (+), subtraction (-), multiplication (*), division (/), and modulus (%) operations. Note: They behave differently when used with non-numeric column types. 
Let's now find the top 5 states by population growth between 2000 and 2008.

## Instructions
* Define a select statement called stmt to return:
* i) The state column of the census table (census.columns.state). 
* ii) The difference in population count between 2008 (census.columns.pop2008) and 2000 (census.columns.pop2000) labeled as 'pop_change'.
* Group the statement by census.columns.state.
* Order the statement by population change ('pop_change') in descending order. Do so by passing it desc('pop_change').
* Use the .limit() method on the statement to return only 5 records.
* Execute the statement and fetchall the records.
* The print statement has already been written for you. Hit 'Submit Answer' to view the results!

```python

# Build query to return state names by population difference from 2008 to 2000: stmt
stmt = select([census.columns.state, (census.columns.pop2008- census.columns.pop2000).label('pop_change')])

# Append group by for the state: stmt
stmt = stmt.group_by(census.columns.state)

# Append order by for pop_change descendingly: stmt
stmt = stmt.order_by(desc('pop_change'))

# Return only 5 results: stmt
stmt = stmt.limit(5)

# Use connection to execute the statement and fetch all results
results = connection.execute(stmt).fetchall()

# Print the state and population change for each record
for result in results:
    print('{}:{}'.format(result.state, result.pop_change))
```
# Determining the Overall Percentage of Females
It's possible to combine functions and operators in a single select statement as well. These combinations can be exceptionally handy when we want to calculate percentages or averages, and we can also use the case() expression to operate on data that meets specific criteria while not affecting the query as a whole. The case() expression accepts a list of conditions to match and the column to return if the condition matches, followed by an else_ if none of the conditions match. We can wrap this entire expression in any function or math operation we like. 
Often when performing integer division, we want to get a float back. While some databases will do this automatically, you can use the cast() function to convert an expression to a particular type.


## Instructions
* Import case, cast, and Float from sqlalchemy.
* Build an expression female_pop2000to calculate female population in 2000. To achieve this:
* Use case() inside func.sum().
* The first argument of case() is a list containing a tuple of 
* i) A boolean checking that census.columns.sex is equal to 'F'.
* ii) The column census.columns.pop2000.
* The second argument is the else_ condition, which should be set to 0.
* Calculate the total population in 2000 and use cast() to convert it to Float.
* Build a query to calculate the percentage of females in 2000. To do this, divide female_pop2000 by total_pop2000 and multiply by 100.
* Execute the query and print percent_female.

```python

# import case, cast and Float from sqlalchemy
from sqlalchemy import case, cast, Float

# Build an expression to calculate female population in 2000
female_pop2000 = func.sum(
    case([
        (census.columns.sex == 'F', census.columns.pop2000)
    ], else_=0))

# Cast an expression to calculate total population in 2000 to Float
total_pop2000 = cast(func.sum(census.columns.pop2000), Float)

# Build a query to calculate the percentage of females in 2000: stmt
stmt = select([female_pop2000 / total_pop2000 * 100])

# Execute the query and store the scalar result: percent_female
percent_female = connection.execute(stmt).scalar()

# Print the percentage
print(percent_female)
```
# Automatic Joins with an Established Relationship
If you have two tables that already have an established relationship, you can automatically use that relationship by just adding the columns we want from each table to the select statement. Recall that Jason constructed the following query:

```code
stmt = select([census.columns.pop2008, state_fact.columns.abbreviation])
```

in order to join the census and state_fact tables and select the pop2008 column from the first and the abbreviation column from the second. In this case, the census and state_fact tables had a pre-defined relationship: the state column of the former corresponded to the name column of the latter.
In this exercise, you'll use the same predefined relationship to select the pop2000 and abbreviation columns!

## instructions
Build a statement to join the census and state_fact tables and select the pop2000 column from the first and the abbreviation column from the second.
Execute the statement to get the first result and save it as result.
Hit 'Submit Answer' to loop over the keys of the result object, and print the key and value for each!

```python

# Build a statement to join census and state_fact tables: stmt
stmt = select([census.columns.pop2000, state_fact.columns.abbreviation ])

# Execute the statement and get the first result: result
result = connection.execute(stmt).first()

# Loop over the keys in the result object and print the key and value
for key in result.keys():
    print(key, getattr(result, key))
```
# Joins
If you aren't selecting columns from both tables or the two tables don't have a defined relationship, you can still use the .join() method on a table to join it with another table and get extra data related to our query. The join() takes the table object you want to join in as the first argument and a condition that indicates how the tables are related to the second argument. Finally, you use the .select_from() method on the select statement to wrap the join clause. For example, in the video, Jason executed the following code to join the census table to the state_fact table such that the state column of the census table corresponded to the name column of the state_fact table.

```code

stmt = stmt.select_from(
    census.join(
        state_fact, census.columns.state == 
        state_fact.columns.name)
```
## instructions
* Build a statement to select ALL the columns from the census and state_fact tables. To select ALL the columns from two tables employees and sales, for example, you would use stmt = select([employees, sales]).
* Append a select_from to stmt to join the census table to the state_fact table by the state column in census and the name column in the state_fact table.
* Execute the statement to get the first result and save it as result. This code is already written.
* Hit 'Submit Answer' to loop over the keys of the result object, and print the key and value for each!

```python

# Build a statement to select the census and state_fact tables: stmt
stmt = select([census, state_fact])

# Add a select_from clause that wraps a join for the census and state_fact
# tables where the census state column and state_fact name column match
stmt = stmt.select_from(
    census.join(state_fact, census.columns.state == state_fact.columns.name))

# Execute the statement and get the first result: result
result = connection.execute(stmt).first()

# Loop over the keys in the result object and print the key and value
for key in result.keys():
    print(key, getattr(result, key))
```
# More Practice with Joins
You can use the same select statement you built in the last exercise, however, let's add a twist and only return a few columns and use the other table in a group_by() clause.

## instructions
* Build a statement to select:
* The state column from the census table. 
* The sum of the pop2008 column from the census table. 
* The census_division_name column from the state_fact table.
* Append a .select_from() to stmt in order to join the census and state_fact tables by the state and name columns.
* Group the statement by the name column of the state_fact table.
* Execute the statement to get all the records and save it as results.
* Hit 'Submit Answer' to loop over the results object and print each record.

```python

# Build a statement to select the state, sum of 2008 population and census
# division name: stmt
stmt = select([
    census.columns.state,
    func.sum(census.columns.pop2008),
    state_fact.columns.census_division_name
])

# Append select_from to join the census and state_fact tables by the census state and state_fact name columns
stmt = stmt.select_from(
    census.join(state_fact, census.columns.state == state_fact.columns.name)
)

# Append a group by for the state_fact name column
stmt = stmt.group_by(state_fact.columns.name)

# Execute the statement and get the results: results
results = connection.execute(stmt).fetchall()

# Loop over the results object and print each record.
for record in results:
    print(record)

```
# Using alias to handle same table joined queries
Often, you'll have tables that contain hierarchical data, such as employees and managers who are also employees. For this reason, you may wish to join a table to itself on different columns. The .alias() method, which creates a copy of a table, helps accomplish this task. Because it's the same table, you only need a where clause to specify the join condition. 
Here, you'll use the .alias() method to build a query to join the employees table against itself to determine to whom everyone reports.

## instructions
Save an alias of the employees table as managers. To do so, apply the method .alias() to employees.
Build a query to select the employee name and their manager's name. The manager's name has already been selected for you. Use label to label the name column of employees as 'employee'.
Append a where clause to stmt to match where the id column of the managers table corresponds to the mgr column of the employees table.
Order the statement by the name column of the managers table.
Execute the statement and store all the results. This code is already written. Hit 'Submit Answer' to print the names of the managers and all their employees.

```python

# Make an alias of the employees table: managers
managers = employees.alias()

# Build a query to select manager's and their employees names: stmt
stmt = select(
    [managers.columns.name.label('manager'),
     employees.columns.name.label('employee')]
)

# Match managers id with employees mgr: stmt
stmt = stmt.where(managers.columns.id == employees.columns.mgr)

# Order the statement by the managers name: stmt
stmt = stmt.order_by(managers.columns.name)

# Execute statement: results
results = connection.execute(stmt).fetchall()

# Print records
for record in results:
    print(record)
```
# Leveraging Functions and Group_bys with Hierarchical Data
It's also common to want to roll up data which is in a hierarchical table. Rolling up data requires making sure you're careful which alias you use to perform the group_bys and which table you use for the function. 
Here, your job is to get a count of employees for each manager.

## Instructions
* Save an alias of the employees table as managers.
* Build a query to select the name column of the managers table and the count of the number of their employees. The function func.count() has been imported and will be useful! Use it to count the id column of the employees table.
* Using a .where() clause, filter the records where the id column of the managers table and mgr column of the employees table are equal.
* Group the query by the name column of the managers table.
* Execute the statement and store all the results. Print the names of the managers and their employees. This code has already been written so hit 'Submit Answer' and check out the results!

```python

# Make an alias of the employees table: managers
managers = employees.alias()

# Build a query to select manager's and their employees names: stmt
stmt = select([managers.columns.name, func.count(employees.columns.id)])

# Append a where clause that ensures the manager id and employee mgr are equal
stmt = stmt.where(managers.columns.id == employees.columns.mgr)

# Group by Managers Name
stmt = stmt.group_by(managers.columns.name)

# Execute statement: results
results = connection.execute(stmt).fetchall()

# print manager
for record in results:
    print(record)
```
# Working on Blocks of Records
Fantastic work so far! As Jason discussed in the video, sometimes you may have the need to work on a large ResultProxy, and you may not have the memory to load all the results at once. To work around that issue, you can get blocks of rows from the ResultProxy by using the .fetchmany() method inside a loop. With .fetchmany(), give it an argument of the number of records you want. When you reach an empty list, there are no more rows left to fetch, and you have processed all the results of the query. Then you need to use the .close() method to close out the connection to the database.
You'll now have the chance to practice this on a large ResultProxy called results_proxy that has been pre-loaded for you to work with.

## Instructions
* Use a while loop that checks if there are more_results.
* Inside the loop, apply the method .fetchmany() to results_proxy to get 50 records at a time and store those records as partial_results.
* After fetching the records, if partial_results is an empty list (that is, if it is equal to []), set more_results to False.
* Loop over the partial_results and, if row.state is a key in the state_count dictionary, increment state_count[row.state] by 1; otherwise set state_count[row.state] to 1.
* After the while loop, close the ResultProxy results_proxy using .close().
* Hit 'Submit Answer' to print state_count.

```python

# Start a while loop checking for more results
while more_results:
    # Fetch the first 50 results from the ResultProxy: partial_results
    partial_results = results_proxy.fetchmany(50)

    # if empty list, set more_results to False
    if partial_results == []:
        more_results = False

    # Loop over the fetched records and increment the count for the state
    for row in partial_results:
        if row.state in state_count:
            state_count[row.state] += 1
        else:
            state_count[row.state] = 1

# Close the ResultProxy, and thus the connection
results_proxy.close()

# Print the count by state
print(state_count)
```
# Creating Tables with SQLAlchemy
Previously, you used the Table object to reflect a table from an existing database, but what if you wanted to create a new table? You'd still use the Table object; however, you'd need to replace the autoload and autoload_with parameters with Column objects.
The Column object takes a name, a SQLAlchemy type with an optional format, and optional keyword arguments for different constraints. 
When defining the table, recall how in the video Jason passed in 255 as the maximum length of a String by using Column('name', String(255)). Checking out the slides from the video may help: you can download them by clicking on 'Slides' next to the IPython Shell.
After defining the table, you can create the table in the database by using the .create_all() method on metadata and supplying the engine as the only parameter. Go for it!

## instructions
* Import Table, Column, String, Integer, Float, Boolean from sqlalchemy.
* Build a new table called data with columns 'name' (String(255)), 'count' (Integer()), 'amount'(Float()), and 'valid' (Boolean()) columns. The second argument of Table() needs to be metadata, which has already been initialized.
* Create the table in the database by passing engine to metadata.create_all().


```python

# Import Table, Column, String, Integer, Float, Boolean from sqlalchemy
from sqlalchemy import Table, Column, String, Integer, Float, Boolean

# Define a new table with a name, count, amount, and valid column: data
data = Table('data', metadata,
             Column('name', String(255)),
             Column('count', Integer()),
             Column('amount', Float()),
             Column('valid', Boolean())
)

# Use the metadata to create the table
metadata.create_all(engine)

# Print table details
print(repr(data))
```

# Constraints and Data Defaults

You're now going to practice creating a table with some constraints! Often, you'll need to make sure that a column is unique, nullable, a positive value, or related to a column in another table. This is where constraints come in.
As Jason showed you in the video, in addition to constraints, you can also set a default value for the column if no data is passed to it via the default keyword on the column.


Table, Column, String, Integer, Float, Boolean are already imported from sqlalchemy.
Build a new table called data with a unique name (String), count (Integer) defaulted to 1, amount (Float), and valid (Boolean) defaulted to False.
Hit 'Submit Answer' to create the table in the database and to print the table details for data.

```python

# Import Table, Column, String, Integer, Float, Boolean from sqlalchemy
from sqlalchemy import Table, Column, String, Integer, Float, Boolean

# Define a new table with a name, count, amount, and valid column: data
data = Table('data', metadata,
             Column('name', String(255), unique=True),
             Column('count', Integer(), default=1),
             Column('amount', Float()),
             Column('valid', Boolean(), default=False)
)

# Use the metadata to create the table
metadata.create_all(engine)

# Print the table details
print(repr(metadata.tables['data']))
```
# Inserting a single row with an insert() statement
There are several ways to perform an insert with SQLAlchemy; however, we are going to focus on the one that follows the same pattern as the select statement. 
It uses an insert statement where you specify the table as an argument, and supply the data you wish to insert into the value via the .values() method as keyword arguments.
Here, the name of the table is data.

## Instructions

Import insert and select from the sqlalchemy module.
Build an insert statement for the data table to set name to 'Anna', count to 1, amount to 1000.00, and valid to True. Save the statement as stmt.
Execute stmt with the connection and store the results.
Print the rowcount attribute of results to see how many records were inserted.
Build a select statement to query for the record with the name of 'Anna'.
Hit 'Submit Answer' to print the results of executing the select statement.

```python

# Import insert and select from sqlalchemy
from sqlalchemy import insert , select

# Build an insert statement to insert a record into the data table: stmt
stmt = insert(data).values(name='Anna', count=1, amount=1000.00, valid=True)

# Execute the statement via the connection: results
results = connection.execute(stmt)

# Print result rowcount
print(results.rowcount)

# Build a select statement to validate the insert
stmt = select([data]).where(data.columns.name == 'Anna')

# Print the result of executing the query.
print(connection.execute(stmt).first())
```

# Inserting Multiple Records at Once
It's time to practice inserting multiple records at once! 
As Jason showed you in the video, you'll want to first build a list of dictionaries that represents the data you want to insert. Then, in the .execute() method, you can pair this list of dictionaries with an insert statement, which will insert all the records in your list of dictionaries

## Instructions
* Build a list of dictionaries called values_list with two dictionaries. In the first dictionary set name to 'Anna', count to 1, amount to 1000.00, and valid to True. In the second dictionary of the list, set name to 'Taylor', count to 1, amount to 750.00, and valid to False.
* Build an insert statement for the data table for a multiple insert, save it as stmt.
* Execute stmt with the values_list via connection and store the results. Make sure values_list is the second argument to .execute().
* Print the rowcount of the results

```python

# Build a list of dictionaries: values_list
values_list = [
    {'name': 'Anna', 'count': 1, 'amount': 1000.00, 'valid': True},
    {'name': 'Taylor', 'count': 1, 'amount': 750.00, 'valid': False}
]

# Build an insert statement for the data table: stmt
stmt = insert(data)

# Execute stmt with the values_list: results
results = connection.execute(stmt, values_list)

# Print rowcount
print(results.rowcount)
```
# Loading a CSV into a Table
You've done a great job so far at inserting data into tables! You're now going to learn how to load the contents of a CSV file into a table.
We have used the csv module to set up a csv_reader, which is just a reader object that can iterate over the lines in a given CSV file - in this case, a census CSV file. Using the enumerate() function, you can loop over the csv_reader to handle the results one at a time. Here, for example, the first line it would return is:

```code 
0 ['Illinois', 'M', '0', '89600', '95012']
```
0 is the idx - or line number - while ['Illinois', 'M', '0', '89600', '95012'] is the row, corresponding to the column names 'state' , 'sex', 'age', 'pop2000 'and 'pop2008'. 'Illinois' can be accessed with row[0], 'M' with row[1], and so on. You can create a dictionary containing this information where the keys are the column names and the values are the entries in each line. Then, by appending this dictionary to a list, you can combine it with an insert statement to load it all into a table!

## Instructions
* Create a statement for bulk insert into the census table. To do this, just use insert() and census.
* Create an empty list called values_list and a variable called total_rowcount that is set to 0.
* Within the for loop:
* Complete the data dictionary by filling in the values for each of the keys. The values are contained in row. row[0] represents the value for 'state', row[1] represents the value for 'sex', and so on.
* Append data to values_list.
* If 51 cleanly divides into the current idx:
* Execute stmt with the values_list and save it as results.
* Hit 'Submit Answer' to print total_rowcount when done with all the records.

```python

# Create a insert statement for census: stmt
stmt = insert(census)

# Create an empty list and zeroed row count: values_list, total_rowcount
values_list = []
total_rowcount = 0

# Enumerate the rows of csv_reader
for idx, row in enumerate(csv_reader):
    #create data and append to values_list
    data = {'state': row[0], 'sex': row[1], 'age': row[2], 'pop2000':    row[3], 'pop2008': row[4] }
    values_list.append(data)

    # Check to see if divisible by 51
    if idx % 51 == 0:
        results = connection.execute(stmt, values_list)
        total_rowcount += results.rowcount
        values_list = []

# Print total rowcount
print(total_rowcount)
```
# Updating individual records
The update statement is very similar to an insert statement, except that it also typically uses a where clause to help us determine what data to update. You'll be using the FIPS state code using here, which is appropriated by the U.S. government to identify U.S. states and certain other associated areas. Recall that you can update all wages in the employees table as follows:

```code
stmt = update(employees).values(wage=100.00)
```
For your convenience, the names of the tables and columns of interest in this exercise are: state_fact (Table), name (Column), and fips_state (Column).

## Instructions

Build a statement to select all columns from the state_fact table where the name column is New York. Call it select_stmt.
Print the results of executing the select_stmt and fetching all records.
Build an update statement to change the fips_state column code to 36, save it as stmt.
Use a where clause to filter for states with the name of 'New York' in the state_fact table.
Execute stmt via the connection and save the output as results.
Hit 'Submit Answer' to print the rowcount of the results and the results of executing select_stmt. This will verify the fips_state code is now 36.

```python

# Build a select statement: select_stmt
select_stmt = select([state_fact]).where(state_fact.columns.name == 'New York')

# Print the results of executing the select_stmt
print(connection.execute(select_stmt).fetchall())

# Build a statement to update the fips_state to 36: stmt
stmt = update(state_fact).values(fips_state = 36)

# Append a where clause to limit it to records for New York state
stmt = stmt.where(state_fact.columns.name == 'New York')

# Execute the statement: results
results = connection.execute(stmt)

# Print rowcount
print(results.rowcount)

# Execute the select_stmt again to view the changes
print(connection.execute(select_stmt).fetchall())
```
# Updating Multiple Records

As Jason discussed in the video, by using a where clause that selects more records, you can update multiple records at once. It's time now to practice this!
For your convenience, the names of the tables and columns of interest in this exercise are: state_fact (Table), notes (Column), and census_region_name (Column).

## Instructions
* Use a where clause to filter for records that have 'West' in the census_region_name column of the state_fact table.
* Execute stmt via the connection and save the output as results.
* Hit 'Submit Answer' to print rowcount of the results

```python

# Build a statement to update the notes to 'The Wild West': stmt
stmt = update(state_fact).values(notes='The Wild West')

stmt = stmt.where(state_fact.columns.census_region_name == 'West')

# Execute the statement: results
results = connection.execute(stmt)

# Print rowcount
print(results.rowcount)
```
# Correlated Updates
You'll be using a flat_census in this exercise as the target of your correlated update. The flat_census table is a summarized copy of your census table.

## Instructions
* Build a statement to select the name column from state_fact. Save the statement as fips_stmt.
* Append a where clause to fips_stmt that matches fips_state from the state_fact table with fips_code in the flat_census table.
* Build an update statement to set the state_name in flat_census to fips_stmt. Save the statement as update_stmt.
* Hit 'Submit Answer' to execute update_stmt, store the results and print the rowcount of results.

```python
# Build a statement to select name from state_fact: stmt
fips_stmt = select([state_fact.columns.name])

# Append a where clause to Match the fips_state to flat_census fips_code
fips_stmt = fips_stmt.where(
    state_fact.columns.fips_state == flat_census.columns.fips_code)

# Build an update statement to set the name to fips_stmt: update_stmt
update_stmt = update(flat_census).values(state_name=fips_stmt)
# Execute update_stmt: results
results = connection.execute(update_stmt)

# Print rowcount
print(results.rowcount)
```
# Deleting all the records from a table
Often, you'll need to empty a table of all of its records so you can reload the data. You can do this with a delete statement with just the table as an argument. For example, in the video, Jason deleted the table extra_employees by executing as follows:
delete_stmt = delete(extra_employees)
Do be careful, though, as deleting cannot be undone!

## Instructions
* Import delete and select from sqlalchemy.
* Build a delete statement to remove all the data from the census table. Save it as stmt.
* Execute stmt via the connection and save the results.
* Hit 'Submit Answer' to select all remaining rows from the census table and print the result to confirm that the table is now empty!

```python

# Import delete, select
from sqlalchemy import delete, select

# Build a statement to empty the census table: stmt
stmt = delete(census)

# Execute the statement: results
results = connection.execute(stmt)

# Print affected rowcount
print(results.rowcount)

# Build a statement to select all records from the census table
stmt = select([census])

# Print the results of executing the statement to verify there are no rows
print(connection.execute(stmt).fetchall())
```

# Deleting specific records
By using a where() clause, you can target the delete statement to remove only certain records. For example, Jason deleted all rows from the employees table that had id 3 with the following delete statement:

```code
delete(employees).where(employees.columns.id == 3
```
Here you'll delete ALL rows which have 'M' in the sex column and 36 in the age column. We have included code at the start which computes the total number of these rows. It is important to make sure that this is the number of rows that you actually delete.
Build a delete statement to remove data from the census table. Save it as stmt_del.
Append a where clause to stmt_del that contains an and_ to filter for rows which have 'M' in the sex column AND 36 in the age column.
Execute the delete statement.
Hit 'Submit Answer' to print the rowcount of the results, as well as to_delete, which returns the number of rows that should be deleted. These should match and this is an important sanity check!

```python
# Build a statement to count records using the sex column for Men (M) age 36: stmt
stmt = select([func.count(census.columns.sex)]).where(
    and_(census.columns.sex == 'M',
         census.columns.age == 36)
)

# Execute the select statement and use the scalar() fetch method to save the record count
to_delete = connection.execute(stmt).scalar()

# Build a statement to delete records for Men (M) age 36: stmt
stmt_del = delete(census)

# Append a where clause to target man age 36
stmt_del = stmt_del.where(
    and_(census.columns.sex == 'M',
         census.columns.age == 36)
)

# Execute the statement: results
results = connection.execute(stmt_del)

# Print affected rowcount and to_delete record count, make sure they match
print(results.rowcount, to_delete)
```
# Deleting a Table Completely
You're now going to practice dropping individual tables from a database with the .drop() method, as well as all tables in a database with the .drop_all() method!
As Spider-Man's Uncle Ben (as well as Jason, in the video!) said: With great power, comes great responsibility. Do be careful when deleting tables, as it's not simple or fast to restore large databases! Remember, you can check to see if a table exists with the .exists() method.
This is the final exercise in this chapter: After this, you'll be ready to apply everything you've learned to a case study in the final chapter of this course!

```python

# Drop the state_fact tables
state_fact.drop(engine)

# Check to see if state_fact exists
print(state_fact.exists(engine))

# Drop all tables
metadata.drop_all(engine)

# Check to see if census exists
print(census.exists(engine))
```
# Setup the Engine and MetaData

In this exercise, your job is to create an engine to the database that will be used in this chapter. Then, you need to initialize its metadata.
Recall how you did this in Chapter 1 by leveraging create_engine() and MetaData.

## Instructions
* Import create_engine and MetaData from sqlalchemy.
* Create an engine to the chapter 5 database by using 'sqlite:///chapter5.sqlite' as the connection string.
* Create a MetaData object as metadata.

```python

# Import create_engine, MetaData
from sqlalchemy import create_engine, MetaData

# Define an engine to connect to chapter5.sqlite: engine
engine = create_engine('sqlite:///chapter5.sqlite')

# Initialize MetaData: metadata
metadata = MetaData()
```
# Create the Table to the Database
Having setup the engine and initialized the metadata, you will now define the census table object and then create it in the database using the metadata and engine from the previous exercise. To create it in the database, you will have to use the .create_all() method on the metadata with engine as the argument.
It may help to refer back to the Chapter 4 exercise in which you learned how to create a table.

## Instructions
* Import Table, Column, String, and Integer from sqlalchemy.
* Define a census table with the following columns:
* 'state' - String - length of 30
* 'sex' - String - length of 1
* 'age' - Integer
* 'pop2000' - Integer
* 'pop2008' - Integer
* Create the table in the database using the metadata and engine.

```python

# Import Table, Column, String, and Integer
from sqlalchemy import Table, Column, String, Integer

# Build a census table: census
census = Table('census', metadata,
               Column('state', String(30)),
               Column('sex', String(1)),
               Column('age', Integer()),
               Column('pop2000', Integer()),
               Column('pop2008', Integer()))

# Create the table in the database
metadata.create_all(engine)
```


















