# Standard Library overview (os, sys)

The standard libraries are very useful because has so many functionalities and allow us find solutions for our codes, we can manipulate as a best way the data and offer quick solutions. 

On the below code is shown a solution called "Web Scraping", it is a code to get and download data from a website in .txt format, just using libraries such as BeautifulSoup and Requests.

> Web scraping is a technique to automatically access and extract large amounts of information from a website, which can save a huge amount of time and effort.
> 

- Firstly we need import the libraries that we will use, BeautifulSoup to convert our data to html format and Request to connect to the URL.
- Secondly we will declare a url variable to save the link that we will use to download the data and then we will try the connection to the URL using  .get().
- Then create an object from BeautifulSoup and convert to HTML format
- Finally create a variable "one_a_tag" to find all the <a> tag use for hyperlinks and add ['href']  to create the hyperlink and at the end create "download_url" variable to concatenate the link created in previous step and save it.

```python
# Import libraries
import requests
import urllib.request
import time
from bs4 import BeautifulSoup

# Set the URL you want to webscrape from
url = 'http://web.mta.info/developers/turnstile.html'

# Connect to the URL
response = requests.get(url)

# Parse HTML and save to BeautifulSoup object¶
soup = BeautifulSoup(response.text, "html.parser")

#If we printed the above object "soup" we see that all the links began in...
# the 38 line
#So we use the .findAll method to search all the lines that start with "a"...
# from line 38 to the end
one_a_tag = soup.findAll('a')[38]
link = one_a_tag['href']

download_url = 'http://web.mta.info/developers/'+ link
urllib.request.urlretrieve(download_url,'./'+link[link.find('/turnstile_')+1:])
```

Comparing the scraped text and the text hosted on the web page, it is completely the same:

![Screen Shot 2021-09-23 at 17.30.10.png](Standard%20Library%20overview%20(os,%20sys)%202c9f63608b7046d296e0c1d82ee85f3c/Screen_Shot_2021-09-23_at_17.30.10.png)

![Screen Shot 2021-09-23 at 17.31.11.png](Standard%20Library%20overview%20(os,%20sys)%202c9f63608b7046d296e0c1d82ee85f3c/Screen_Shot_2021-09-23_at_17.31.11.png)