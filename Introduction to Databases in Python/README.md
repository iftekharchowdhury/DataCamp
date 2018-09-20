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































