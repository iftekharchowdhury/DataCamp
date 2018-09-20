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























