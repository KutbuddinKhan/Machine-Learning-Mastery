
---

# EDA Using Univariate Analysis

This tutorial demonstrates how to perform Univariate Exploratory Data Analysis (EDA) using Seaborn and Matplotlib in Python. Univariate analysis focuses on visualizing and analyzing one variable at a time, providing insights into the data's distribution and characteristics.

## Univariate Analysis:
Univariate analysis involves analyzing a single variable. The primary goal is to understand the distribution, central tendency (mean, median, mode), and dispersion (range, variance, standard deviation) of the data. Examples include histograms, boxplots, and descriptive statistics like mean and standard deviation.

## Prerequisites

Before running the code, ensure you have the following Python libraries installed:

- **pandas**: For data manipulation and analysis.
- **seaborn**: For statistical data visualization.
- **matplotlib**: For creating static, animated, and interactive visualizations.

You can install these libraries using `pip`:

```bash
pip install pandas seaborn matplotlib
```

## Code Overview

The following code examples illustrate how to use Seaborn and Matplotlib to visualize and analyze the distribution of both categorical and numerical variables from a dataset.

### 1. Importing Libraries

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

- **pandas**: Used for data manipulation and loading datasets.
- **seaborn**: Provides high-level functions for creating attractive and informative statistical plots.
- **matplotlib**: A plotting library that integrates well with Seaborn for detailed customizations.

### 2. Loading the Dataset

```python
df = pd.read_csv('F:/DATASETS/train.csv')
df.head()
```

- **df.head()**: Displays the first 5 rows of the dataset to get an initial understanding of the data.

### 3. Analyzing Categorical Data

Univariate analysis of categorical data focuses on visualizing the frequency or proportion of categories within a single variable.

#### a. Countplot

A count plot is useful for visualizing the distribution of categories in a categorical variable.

```python
sns.countplot(x='Survived', data=df)
plt.xlabel('Survived')
plt.ylabel('Count')
plt.show()
```

- **Countplot**: This plot shows the count of occurrences of each category in the `Survived` column. Each bar represents a category and its height corresponds to the count.

To visualize another categorical variable, such as `Pclass`:

```python
sns.countplot(x='Pclass', data=df)
plt.xlabel('Pclass')
plt.ylabel('Count')
plt.show()
```

- **Pclass**: This plot will show the count of passengers in each class (1st, 2nd, 3rd) on the Titanic.

#### b. Pie Chart

A pie chart is used to visualize the proportion of each category within a categorical variable.

```python
df["Survived"].value_counts().plot(kind="pie", autopct='%.2f')
df["Pclass"].value_counts().plot(kind="pie", autopct='%.2f')
```

- **Pie Chart**: Displays the distribution of `Survived` and `Pclass` categories as a percentage of the whole. The `autopct='%.2f'` argument adds percentage labels to the chart.

### 4. Analyzing Numerical Data

Univariate analysis of numerical data involves understanding the distribution and central tendencies of a single numerical variable.

#### a. Histogram

A histogram is used to visualize the frequency distribution of a numerical variable by dividing the data into bins.

```python
plt.hist(df["Age"], bins=5)
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Histogram of Age')
plt.show()
```

- **Histogram**: This plot shows the distribution of ages in the dataset. The data is divided into 5 bins (intervals), and the height of each bin represents the number of data points within that range.

#### b. Distplot

A distplot combines a histogram and a kernel density estimate (KDE) to provide a more comprehensive view of the data distribution.

```python
sns.displot(df['Age'])
```

- **Distplot**: This plot shows the distribution of the `Age` variable along with a KDE line that smooths out the distribution, giving an estimate of the probability density function of the variable.

#### c. Boxplot

A boxplot summarizes the distribution of a numerical variable through its quartiles and highlights potential outliers.

```python
sns.boxplot(df['Age'])
plt.xlabel('Age')
plt.title('Boxplot of Age')
plt.show()
```

- **Boxplot**: This plot displays the median, interquartile range (IQR), and potential outliers in the `Age` column. The box represents the middle 50% of the data, and the lines (whiskers) extend to the smallest and largest values within 1.5 * IQR from the quartiles.

### 5. Descriptive Statistics

Descriptive statistics provide numerical summaries of the distribution and shape of a numerical variable.

```python
df['Age'].min()
df['Age'].max()
df['Age'].mean()
df['Age'].skew()
```

- **min()**: Returns the minimum value in the `Age` column.
- **max()**: Returns the maximum value in the `Age` column.
- **mean()**: Calculates the average value of the `Age` column.
- **skew()**: Measures the asymmetry of the data distribution in the `Age` column. A skewness value close to 0 indicates a symmetric distribution, while positive or negative values indicate skewness.
---
