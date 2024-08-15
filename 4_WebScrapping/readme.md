
---

# Web Scraping Tutorial with Python

This tutorial demonstrates how to scrape data from a website using Python. We will be extracting book titles, prices, images, and availability status from the "Books to Scrape" website.
 
## Prerequisites

Before you begin, make sure you have the following Python libraries installed:

- **pandas**: For data manipulation and analysis.
- **requests**: To send HTTP requests and retrieve web pages.
- **beautifulsoup4**: To parse and navigate HTML documents.
- **lxml**: A parser library that works well with BeautifulSoup for parsing HTML and XML documents.
- **numpy**: For working with arrays (optional in this case, but imported in the script).

You can install these libraries using `pip`:

```bash
pip install pandas requests beautifulsoup4 lxml numpy
```

## Code Explanation

The following is a step-by-step breakdown of the code used to scrape data from the website.

### 1. Importing Necessary Libraries

We start by importing the libraries that will be used for web scraping and data manipulation:

```python
import pandas as pd
import requests
from bs4 import BeautifulSoup
import numpy as np
```

- **pandas**: Although it's not directly used in this code snippet, it could be used later for data manipulation and storage.
- **requests**: Used to send HTTP requests to the website and retrieve the webpage content.
- **BeautifulSoup**: Used to parse the HTML content of the webpage and extract the required information.
- **numpy**: Imported but not directly used in this code. It's a powerful library for numerical computations.

### 2. Defining Headers for the Request

To mimic a request from a web browser and avoid being blocked by the website, we define custom headers:

```python
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.162 Safari/537.36'
}
```

### 3. Sending a GET Request

We send an HTTP GET request to the website and retrieve the webpage content as a string:

```python
webpage = requests.get('https://books.toscrape.com/', headers=headers).text
```

### 4. Parsing the Webpage Content

Using BeautifulSoup, we parse the HTML content retrieved from the webpage:

```python
soup = BeautifulSoup(webpage, 'lxml')
```

- **lxml**: A parser used by BeautifulSoup to parse the HTML document.

### 5. Pretty-Printing the HTML

To view the structure of the parsed HTML, we can use the `prettify()` method:

```python
print(soup.prettify())
```

### 6. Extracting Specific Data

#### a. Extracting the Main Heading (`<h1>`)

To extract the text within the first `<h1>` tag on the page:

```python
soup.find_all('h1')[0].text
```

#### b. Extracting All Book Titles (`<h3>`)

To extract all the book titles, we iterate over the `<h3>` tags:

```python
soup.find_all('h3')
for i in soup.find_all('h3'):
    print(i.text)
```

#### c. Extracting All Paragraph Text (`<p>`)

To extract and print all the text within `<p>` tags:

```python
for i in soup.find_all('p'):
    print(i.text.strip())
```

#### d. Counting Elements by Class

To count the number of elements with a specific class, such as `star-rating` or `price_color`:

```python
len(soup.find_all('p', class_="star-rating"))
len(soup.find_all('p', class_="price_color"))
```

### 7. Extracting Book Information

We extract the book's name, price, image, and availability status:

```python
book = soup.find_all('li', class_="col-xs-6")
len(book)
```

### 8. Storing the Data

We store the extracted data into lists for further processing:

```python
name = []
price = []
images = []
inStocks = []

for i in book:
    name.append(i.find('h3').text.strip())
    price.append(i.find_all('p', class_="price_color")[0].text)
    image = i.find('img', class_='thumbnail')['src']
    images.append(image)
    
    stock_status = i.find('p', class_='availability').text.strip()
    inStocks.append(stock_status)
```

- **name**: A list to store the book titles.
- **price**: A list to store the book prices.
- **images**: A list to store the URLs of the book images.
- **inStocks**: A list to store the availability status of the books.

### 9. Viewing the Extracted Data

Finally, we print the data stored in the lists:

```python
name
price
images
inStocks
```
---
