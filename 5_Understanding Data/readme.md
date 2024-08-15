
---

# Exploratory Data Analysis (EDA) with Pandas

This tutorial demonstrates how to perform basic exploratory data analysis (EDA) on a dataset using Python's Pandas library. EDA is an essential step in understanding the structure, content, and characteristics of your data before applying any modeling techniques.

## Prerequisites

Before running the code, make sure you have the following Python libraries installed:

- **pandas**: A powerful data analysis library that provides data structures like DataFrames.
  
You can install the necessary libraries using `pip`:

```bash
pip install pandas
```

## Step-by-Step EDA

Below is a breakdown of the exploratory data analysis process, including code snippets and explanations.

### 1. Importing the Pandas Library

First, you'll need to import the Pandas library to work with the data.

```python
import pandas as pd
```

### 2. Loading the Dataset

The dataset is loaded into a Pandas DataFrame using the `pd.read_csv()` function. The file path provided should be the location of your CSV file.

```python
df = pd.read_csv('F:/DATASETS/train.csv')
```

### 3. How Big is the Data?

To get a quick overview of the size of the dataset, you can use the `shape` attribute. This will return the number of rows and columns in the DataFrame.

```python
df.shape
```

- **Output**: The shape of the dataset as `(rows, columns)`.
- **Explanation**: This helps you understand the dimensionality of your dataset.

### 4. How Does the Data Look Like?

To take a quick look at the data, you can use the following methods:

#### a. First Few Rows

```python
df.head()
```

- **Output**: The first 5 rows of the dataset.
- **Explanation**: This gives you an initial glimpse into the data.

#### b. Random Sample of Rows

```python
df.sample(5)
```

- **Output**: 5 random rows from the dataset.
- **Explanation**: Random sampling is useful for understanding the distribution of data.

### 5. What is the Data Type of Columns?

Understanding the data types of each column is crucial as it influences how the data can be manipulated.

```python
df.info()
```

- **Output**: Summary of the DataFrame including the data types of each column.
- **Explanation**: This method also shows the non-null count, which is useful for detecting missing values.

### 6. Are There Any Missing Values?

To check for missing values in the dataset, you can use the `isnull()` method combined with `sum()`.

```python
df.isnull().sum()
```

- **Output**: The number of missing values in each column.
- **Explanation**: This is important for data cleaning and deciding how to handle missing data.

### 7. How Does the Data Look Mathematically?

The `describe()` method provides a statistical summary of the numerical columns in the dataset.

```python
df.describe()
```

- **Output**: Statistical summary including mean, standard deviation, min, and max values.
- **Explanation**: This summary helps you understand the central tendency and variability of the data.

### 8. Are There Duplicate Values?

To check for duplicate rows in the dataset:

```python
df.duplicated().sum()
```

- **Output**: The number of duplicate rows.
- **Explanation**: Removing duplicates is important to avoid redundancy and potential bias in analysis.

### 9. How is the Correlation Between Columns?

Correlation helps you understand the relationship between different columns in your dataset. Here, the correlation of all columns with the target column `Survived` is checked:

```python
df.corr()['Survived']
```

- **Output**: Correlation values of each column with the `Survived` column.
- **Explanation**: Correlation values range from -1 to 1, where values closer to 1 or -1 indicate a stronger relationship.
--- 