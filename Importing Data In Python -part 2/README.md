# Importing flat files from the web: your turn!
You are about to import your first file from the web! 
The flat file you will import will be 'winequality-red.csv' from the University of California, Irvine's Machine Learning repository.
The flat file contains tabular data of physiochemical properties of red wine, such as pH, alcohol content and citric acid content,
along with wine quality rating.The URL of the file is

**'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'**
After you import it, you'll check your working directory to confirm that it is there and then you'll load it into a pandas DataFrame.

## Instructions
* Import the function urlretrieve from the subpackage urllib.request.
* Assign the URL of the file to the variable url.
* Use the function urlretrieve() to save the file locally as 'winequality-red.csv'.
* Execute the remaining code to load 'winequality-red.csv' in a pandas DataFrame and to print its head to the shell.

```python

# Import package
from urllib.request import urlretrieve

# Import pandas
import pandas as pd

# Assign url of file: url
url =  'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'

# Save file locally
urlretrieve(url,'winequality-red.csv')

# Read file into a DataFrame and print its head
df = pd.read_csv('winequality-red.csv', sep=';')
print(df.head())
```
# Opening and reading flat files from the web
You have just imported a file rom the web, saved it locally and loaded it into a DataFrame. If you just wanted to load a file from the web into a DataFrame without first saving it locally, you can do that easily using pandas. In particular, you can use the function pd.read_csv() with the URL as the first argument and the separator sep as the second argument.

The URL of the file, once again, is
**'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'**
## Instructions
* Assign the URL of the file to the variable url.
* Read file into a DataFrame df using pd.read_csv(), recalling that the separator in the file is ';'.
* Print the head of the DataFrame df.
* Execute the rest of the code to plot histogram of the first feature in the DataFrame df.

```python

# Import packages
import matplotlib.pyplot as plt
import pandas as pd

# Assign url of file: url
url = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'

# Read file into a DataFrame: df
df = pd.read_csv(url,';')

# Print the head of the DataFrame
print(df.head())

# Plot first column of df
pd.DataFrame.hist(df.ix[:, 0:1])
plt.xlabel('fixed acidity (g(tartaric acid)/dm$^3$)')
plt.ylabel('count')
plt.show()
```
# Importing non-flat files from the web
Congrats! You've just loaded a flat file from the web into a DataFrame without first saving it locally using the pandas function pd.read_csv(). This function is super cool because it has close relatives that allow you to load all types of files, not only flat ones. In this interactive exercise, you'll use pd.read_excel() to import an Excel spreadsheet.

The URL of the spreadsheet is
'http://s3.amazonaws.com/assets.datacamp.com/course/importing_data_into_r/latitude.xls'
Your job is to use pd.read_excel() to read in all of its sheets, print the sheet names and then print the head of the first sheet using its name, not its index.
Note that the output of pd.read_excel() is a Python dictionary with sheet names as keys and corresponding DataFrames as corresponding values.

## Instructions
* Assign the URL of the file to the variable url.
* Read the file in url into a dictionary xl using pd.read_excel() recalling that, in order to import all sheets you need to pass None to the argument sheetname.
* Print the names of the sheets in the Excel spreadsheet; these will be the keys of the dictionary xl.
* Print the head of the first sheet using the sheet name, not the index of the sheet! The sheet name is '1700'

# Performing HTTP requests in Python using urllib
Now that you know the basics behind HTTP GET requests, it's time to perform some of your own. In this interactive exercise, you will ping our very own DataCamp servers to perform a GET request to extract information from our teach page, 
"http://www.datacamp.com/teach/documentation"
In the next exercise, you'll extract the HTML itself. Right now, however, you are going to package and send the request and then catch the response.

## Instructions
* Import the functions urlopen and Request from the subpackage urllib.request.
* Package the request to the url "http://www.datacamp.com/teach/documentation" using the function Request() and assign it to request.
* Send the request and catch the response in the variable response with the function urlopen().
* Run the rest of the code to see the datatype of response and to close the connection!

```python

# Import packages
from urllib.request import Request, urlopen

# Specify the url
url = "http://www.datacamp.com/teach/documentation"

# This packages the request: request
request = Request(url)

# Sends the request and catches the response: response
response = urlopen(request)

# Print the datatype of response
print(type(response))

# Be polite and close the response!
response.close()
```
# Printing HTTP request results in Python using urllib
You have just packaged and sent a GET request to "http://www.datacamp.com/teach/documentation" and then caught the response. You saw that such a response is a http.client.HTTPResponse object. The question remains: what can you do with this response?
Well, as it came from an HTML page, you could read it to extract the HTML and, in fact, such a http.client.HTTPResponse object has an associated read() method. In this exercise, you'll build on your previous great work to extract the response and print the HTML.

## Instructions
* Send the request and catch the response in the variable response with the function urlopen(), as in the previous exercise.
* Extract the response using the read() method and store the result in the variable html.
* Print the string html.
* Hit submit to perform all of the above and to close the response: be tidy!

```python

# Import packages
from urllib.request import urlopen, Request

# Specify the url
url = "http://www.datacamp.com/teach/documentation"

# This packages the request
request = Request(url)

# Sends the request and catches the response: response
response = urlopen(request)

# Extract the response: html
html = response.read()

# Print the html
print (html)

# Be polite and close the response!
response.close()
```
# Performing HTTP requests in Python using requests
Now that you've got your head and hands around making HTTP requests using the urllib package, you're going to figure out how to do the same using the higher-level requests library. You'll once again be pinging DataCamp servers for their "http://www.datacamp.com/teach/documentation" page.
Note that unlike in the previous exercises using urllib, you don't have to close the connection when using requests!

## Instructions
* Import the package requests.
* Assign the URL of interest to the variable url.
* Package the request to the URL, send the request and catch the response with a single function requests.get(), assigning the response to the variable r.
* Use the text attribute of the object r to return the HTML of the webpage as a string; store the result in a variable text.
* Hit submit to print the HTML of the webpage.

```python

# Import package
from urllib.request import Request,urlopen
import requests

# Specify the url: url
url = "http://www.datacamp.com/teach/documentation"

# Packages the request, send the request and catch the response: r
r = requests.get(url)
# Extract the response: text
text = r.text

# Print the html
print(text)
```
# Parsing HTML with BeautifulSoup
In this interactive exercise, you'll learn how to use the BeautifulSoup package to parse, prettify and extract information from HTML. You'll scrape the data from the webpage of Guido van Rossum, Python's very own Benevolent Dictator for Life. In the following exercises, you'll prettify the HTML and then extract the text and the hyperlinks.
The URL of interest is url = 'https://www.python.org/~guido/'.

## Instructions
* Import the function BeautifulSoup from the package bs4.
* Assign the URL of interest to the variable url.
* Package the request to the URL, send the request and catch the response with a single function requests.get(), assigning the response to the variable r.
* Use the text attribute of the object r to return the HTML of the webpage as a string; store the result in a variable html_doc.
* Create a BeautifulSoup object soup from the resulting HTML using the function BeautifulSoup().
* Use the method prettify() on soup and assign the result to pretty_soup.
* Hit submit to print to prettified HTML to your shell!

```python

# Import packages
import requests
from bs4 import BeautifulSoup 

# Specify url: url
url = 'https://www.python.org/~guido/'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Extracts the response as html: html_doc

html_doc = r.text
# Create a BeautifulSoup object from the HTML: soup
soup = BeautifulSoup(html_doc)

# Prettify the BeautifulSoup object: pretty_soup
pretty_soup = BeautifulSoup.prettify(soup)

# Print the response
print(pretty_soup)
```
# Turning a webpage into data using BeautifulSoup: getting the text
As promised, in the following exercises, you'll learn the basics of extracting information from HTML soup. In this exercise, you'll figure out how to extract the text from the BDFL's webpage, along with printing the webpage's title.

## Instructions

* In the sample code, the HTML response object html_doc has already been created: your first task is to Soupify it using the function BeautifulSoup() and to assign the resulting soup to the variable soup.
* Extract the title from the HTML soup soup using the attribute title and assign the result to guido_title.
* Print the title of Guido's webpage to the shell using the print() function.
* Extract the text from the HTML soup soup using the method get_text() and assign to guido_text.
* Hit submit to print the text from Guido's webpage to the shell.

```python

# Import packages
import requests
from bs4 import BeautifulSoup

# Specify url: url
url = 'https://www.python.org/~guido/'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Extract the response as html: html_doc
html_doc = r.text

# Create a BeautifulSoup object from the HTML: soup
soup = BeautifulSoup(html_doc)

# Get the title of Guido's webpage: guido_title
guido_title = soup.title

# Print the title of Guido's webpage to the shell
print (guido_title)

# Get Guido's text: guido_text
guido_text = soup.get_text()

# Print Guido's text to the shell
print(guido_text)
```
# Turning a webpage into data using BeautifulSoup: getting the hyperlinks
In this exercise, you'll figure out how to extract the URLs of the hyperlinks from the BDFL's webpage. In the process, you'll become close friends with the soup method find_all().

## Instructions
* Use the method find_all() to find all hyperlinks in soup, remembering that hyperlinks are defined by the HTML tag <a>; store the result in the variable a_tags.
* The variable a_tags is a results set: your job now is to enumerate over it, using a for loop and to print the actual URLs of the hyperlinks; to do this, for every element link in a_tags, you want to print() link.get('href').

```python

# Import packages
import requests
from bs4 import BeautifulSoup

# Specify url
url = 'https://www.python.org/~guido/'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Extracts the response as html: html_doc
html_doc = r.text

# create a BeautifulSoup object from the HTML: soup
soup = BeautifulSoup(html_doc)

# Print the title of Guido's webpage
print(soup.title)

# Find all 'a' tags (which define hyperlinks): a_tags
a_tags = soup.find_all('a')

# Print the URLs to the shell
for link in a_tags:
    print(link.get('href'))
```
# Loading and exploring a JSON
Now that you know what a JSON is, you'll load one into your Python environment and explore it yourself. Here, you'll load the JSON 'a_movie.json' into the variable json_data, which will be a dictionary. You'll then explore the JSON contents by printing the key-value pairs of json_data to the shell.
## Instructions
* Load the JSON 'a_movie.json' into the variable json_data within the context provided by the with statement. To do so, use the function json.load() within the context manager.
* Use a for loop to print all key-value pairs in the dictionary json_data. Recall that you can access a value in a dictionary using the syntax: dictionary[key].

```python

# Load JSON: json_data
with open("a_movie.json") as json_file:
    json_data = json.load(json_file)

# Print each key-value pair in json_data
for k in json_data.keys():
    print(k + ': ', json_data[k])
```

# API requests

Now it's your turn to pull some movie data down from the Open Movie Database (OMDB) using their API. The movie you'll query the API about is The Social Network. Recall that, in the video, to query the API about the movie Hackers, Hugo's query string was 'http://www.omdbapi.com/?t=hackers' and had a single argument t=hackers.
Note: recently, OMDB has changed their API: you now also have to specify an API key. This means you'll have to add another argument to the URL: apikey=ff21610b.
## Instructions
* Import the requests package.
* Assign to the variable url the URL of interest in order to query 'http://www.omdbapi.com' for the data corresponding to the movie The Social Network. 
* The query string should have two arguments: apikey=ff21610b and t=the+social+network. You can combine them as follows: apikey=ff21610b&t=the+social+network.
* Print the text of the reponse object r by using its text attribute and passing the result to the print() function.

```python

# Import requests package
import requests

# Assign URL to variable: url
url = 'http://www.omdbapi.com?apikey=ff21610b&t=the+social+network'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Print the text of the response
print (r.text)
```
# JSON–from the web to Python
Wow, congrats! You've just queried your first API programmatically in Python and printed the text of the response to the shell. However, as you know, your response is actually a JSON, so you can do one step better and decode the JSON. You can then print the key-value pairs of the resulting dictionary. That's what you're going to do now!

## Instructions
* Pass the variable url to the requests.get() function in order to send the relevant request and catch the response, assigning the resultant response message to the variable r.
* Apply the json() method to the response object r and store the resulting dictionary in the variable json_data.
* Hit Submit Answer to print the key-value pairs of the dictionary json_data to the shell.

```python 

# Import package
import requests

# Assign URL to variable: url
url = 'http://www.omdbapi.com/?apikey=ff21610b&t=social+network'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Decode the JSON data into a dictionary: json_data
json_data = r.json()
print (json_data)
# Print each key-value pair in json_data
for k in json_data.keys():
    print(k + ': ', json_data[k])
```
# Checking out the Wikipedia API
You're doing so well and having so much fun that we're going to throw one more API at you: the Wikipedia API (documented here). You'll figure out how to find and extract information from the Wikipedia page for Pizza. What gets a bit wild here is that your query will return nested JSONs, that is, JSONs with JSONs, but Python can handle that because it will translate them into dictionaries within dictionaries.
The URL that requests the relevant query from the Wikipedia API is
https://en.wikipedia.org/w/api.php?action=query&prop=extracts&format=json&exintro=&titles=pizza

## Instructions
* Assign the relevant URL to the variable url.
* Apply the json() method to the response object r and store the resulting dictionary in the variable json_data.
* The variable pizza_extract holds the HTML of an extract from Wikipedia's Pizza page as a string; use the function print() to print this string to the shell.

```python

# Import package
import requests

# Assign URL to variable: url
url = 'https://en.wikipedia.org/w/api.php?action=query&prop=extracts&format=json&exintro=&titles=pizza'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Decode the JSON data into a dictionary: json_data
json_data = r.json() 

# Print the Wikipedia page extract
pizza_extract = json_data['query']['pages']['24768']['extract']
print(pizza_extract)
```
# API Authentication
The package tweepy is great at handling all the Twitter API OAuth Authentication details for you. All you need to do is pass it your authentication credentials. In this interactive exercise, we have created some mock authentication credentials (if you wanted to replicate this at home, you would need to create a Twitter App as Hugo detailed in the video). Your task is to pass these credentials to tweepy's OAuth handler.

## Instructions
* Import the package tweepy.
* Pass the parameters consumer_key and consumer_secret to the function tweepy.OAuthHandler().
* Complete the passing of OAuth credentials to the OAuth handler auth by applying to it the method set_access_token(), along with arguments access_token and access_token_secret.

```python

# Import package
import tweepy

# Store OAuth authentication credentials in relevant variables
access_token = "1092294848-aHN7DcRP9B4VMTQIhwqOYiB14YkW92fFO8k8EPy"
access_token_secret = "X4dHmhPfaksHcQ7SCbmZa2oYBBVSD2g8uIHXsp5CTaksx"
consumer_key = "nZ6EA0FxZ293SxGNg8g8aP0HM"
consumer_secret = "fJGEodwe3KiKUnsYJC3VRndj7jevVvXbK2D5EiJ2nehafRgA6i"

# Pass OAuth details to tweepy's OAuth handler
auth = tweepy.OAuthHandler(consumer_key, consumer_secret )
auth.set_access_token(access_token,access_token_secret)
print (auth)
```
# Streaming tweets











