
--- 

# Pandas CSV Operations Tutorial

This tutorial provides a comprehensive guide on various operations you can perform with CSV files using the Pandas library in Python. Below are the steps with explanations and examples.

## 1. Import Pandas

To get started, import the Pandas library, which is essential for handling CSV files and performing data analysis.

```python
import pandas as pd
```

## 2. Opening a Local CSV File

To read a CSV file that is stored locally on your machine, use the `pd.read_csv()` function and pass the file path as an argument.

```python
df = pd.read_csv('aug_train.csv')
```

## 3. Opening a CSV File from an URL

You can also read a CSV file directly from an online URL. Here, we use the `requests` library to fetch the content and the `StringIO` class to handle it as a file-like object.

```python
import requests
from io import StringIO

url = "https://raw.githubusercontent.com/cs109/2014_data/master/countries.csv"

headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:66.0) Gecko/20100101 Firefox/66.0"}
req = requests.get(url, headers=headers)
data = StringIO(req.text)

pd.read_csv(data)
```

## 4. Sep Parameter

If your CSV file uses a separator other than a comma, you can specify it using the `sep` parameter. For example, to read a tab-separated file:

```python
pd.read_csv("movie_titles_metadata.tsv", sep='\t', names=["sno", "name", "release_year", "rating", "votes", "genres"])
```

## 5. Index_col Parameter

Use the `index_col` parameter to set a specific column as the index for the DataFrame.

```python
pd.read_csv('aug_train.csv', index_col="enrollee_id")
```

## 6. Header Parameter

The `header` parameter is used when the first row of your CSV file is not the actual header. You can skip to the correct row using this parameter.

```python
pd.read_csv("test.csv", header=1)
```

## 7. Use_cols Parameter

If you only need to load specific columns from a CSV file, use the `usecols` parameter to select them.

```python
pd.read_csv('aug_train.csv', usecols=['enrollee_id', 'gender', 'education_level'])
```

## 8. Squeeze Parameter

The `squeeze` parameter returns a Series if the DataFrame has only one column. This can be useful for simplifying your data structures.

```python
pd.read_csv('aug_train.csv', usecols=["enrollee_id"], squeeze=True)
```

## 9. Skiprows/nrows Parameter

- **Skiprows**: Use this parameter to skip specific rows when reading a CSV file.

    ```python
    pd.read_csv("aug_train.csv", skiprows=[0, 5])
    ```

- **nrows**: Use this parameter to read only a specific number of rows.

    ```python
    pd.read_csv("aug_train.csv", nrows=100)
    ```

## 10. Encoding Parameter

If your CSV file uses a different encoding, specify it with the `encoding` parameter.

```python
pd.read_csv("zomato.csv", encoding='latin-1')
```

## 11. Skip Bad Lines

To handle corrupted or improperly formatted lines in your CSV file, use the `error_bad_lines` parameter and set it to `False`.

```python
pd.read_csv("", sep=';', encoding='latin-1', error_bad_lines=False)
```

## 12. Dtypes Parameter

To enforce specific data types for certain columns, use the `dtype` parameter. This is useful for ensuring consistency in your data.

```python
pd.read_csv("aug_train.csv", dtype={'target': int}).info()
```

## 13. Handling Dates

To automatically parse dates when reading your CSV file, use the `parse_dates` parameter. This helps in converting date strings into Pandas `datetime` objects.

```python
pd.read_csv("IPL Matches 2008-2020.csv", parse_dates=['date']).info()
```

## 14. Converters

You can apply custom functions to specific columns using the `converters` parameter. Below is an example where team names are converted to their abbreviations.

```python
def rename(name):
    if name == "Royal Challengers Bangalore":
        return "RCB"
    elif name == "Mumbai Indians":
        return "MI"
    elif name == "Chennai Super Kings":
        return "CSK"
    elif name == "Delhi Daredevils":
        return "DC"
    else:
        return name

pd.read_csv("IPL Matches 2008-2020.csv", converters={"team1": rename})
```

## 15. na_values Parameter

The `na_values` parameter allows you to specify additional strings to recognize as NA/NaN.

```python
pd.read_csv("aug_train.csv", na_values=['Male'])
```

## 16. Loading a Huge Dataset in Chunks

For handling very large datasets, you can load them in chunks using the `chunksize` parameter. This reads the file in smaller, manageable parts.

```python
df = pd.read_csv("aug_train.csv", chunksize=5000)
for chunk in df:
    print(chunk.shape)
```
---