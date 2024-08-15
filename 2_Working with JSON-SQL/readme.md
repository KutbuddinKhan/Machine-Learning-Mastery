
---

# Pandas JSON and SQL Operations Tutorial
 
This tutorial provides a guide on working with JSON and SQL databases using the Pandas library in Python. Below, you'll find explanations for reading JSON data from both local files and online APIs, as well as interacting with SQL databases to query data. 

## Requirements

Before you begin, ensure you have the following Python libraries installed:

- **pandas**: For handling and analyzing data.
- **mysql-connector-python**: To connect and interact with MySQL databases.
- **requests**: (Optional) Useful for making HTTP requests if you're fetching JSON from a web API.

You can install these libraries using `pip`:

```bash
pip install pandas mysql-connector-python requests
```

## 1. Importing Pandas

First, you'll need to import the Pandas library, which will be used for data manipulation and analysis.

```python
import pandas as pd
```

## 2. Working with JSON Files

Pandas makes it easy to work with JSON files. You can read a JSON file from a local path or directly from a URL.

### a. Reading a Local JSON File

To read a JSON file stored locally on your machine, use the `pd.read_json()` function and provide the file path.

```python
df = pd.read_json("F:/DATASETS/train.json")
```

### b. Reading a JSON from an Online API

You can also read JSON data directly from an online API by passing the URL to the `pd.read_json()` function.

```python
df = pd.read_json('https://api.exchangerate-api.com/v4/latest/INR')
```

This method is useful for working with real-time data, such as currency exchange rates, weather data, or other JSON-formatted APIs.

## 3. Working with SQL Databases

Pandas can also be used to interact with SQL databases, allowing you to run SQL queries and directly load the results into a DataFrame.

### a. Importing the MySQL Connector

First, you need to import the `mysql.connector` module, which allows you to connect to a MySQL database.

```python
import mysql.connector
```

### b. Establishing a Connection to the Database

You'll need to set up a connection to your MySQL database by providing the host, username, password, and the database name. Here's an example of how to connect to a MySQL database called `ecommerce`:

```python
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="",
    database="ecommerce",
    auth_plugin='mysql_native_password'
)
```

### c. Querying Data from the SQL Database

Once the connection is established, you can run SQL queries using `pd.read_sql_query()` to load data into a Pandas DataFrame. Here's an example where we're selecting customers from a specific state:

```python
df = pd.read_sql_query("SELECT * FROM ecommerce.customers WHERE customer_state='SP'", conn)
df
```

This will load the result of the SQL query into a DataFrame, allowing you to work with the data directly in Pandas.

## 4. Additional Notes

- **Closing the Connection**: After performing the necessary operations, always close the database connection to free up resources.

```python
conn.close()
```
---