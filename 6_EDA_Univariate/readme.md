
---

# Data Visualization with Seaborn and Matplotlib

This tutorial demonstrates how to visualize data using Seaborn and Matplotlib in Python. We'll cover various types of plots to analyze categorical and numerical data from a dataset.

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

The following code examples illustrate how to use Seaborn and Matplotlib to visualize different aspects of the dataset.

### 1. Importing Libraries

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

- **pandas**: Used for data manipulation.
- **seaborn**: Provides high-level functions for creating statistical plots.
- **matplotlib**: Provides functions for creating a wide range of plots.

### 2. Loading the Dataset

```python
df = pd.read_csv('F:/DATASETS/train.csv')
df.head()
```

- **df.head()**: Displays the first 5 rows of the dataset to get an overview of the data.

### 3. Analyzing Categorical Data

#### a. Countplot

To visualize the distribution of categorical variables, we use a count plot.

```python
sns.countplot(x='Survived', data=df)
plt.xlabel('Survived')
plt.ylabel('Count')
plt.show()
```

- **Countplot**: Shows the count of observations in each categorical bin using bars.

You can also visualize the distribution of another categorical variable, such as `Pclass`:

```python
sns.countplot(x='Pclass', data=df)
plt.xlabel('Pclass')
plt.ylabel('Count')
plt.show()
```

#### b. Pie Chart

To visualize the proportions of categorical data, use a pie chart.

```python
df["Survived"].value_counts().plot(kind="pie", autopct='%.2f')
df["Pclass"].value_counts().plot(kind="pie", autopct='%.2f')
```

- **Pie Chart**: Displays the percentage distribution of each category in a circular format.

### 4. Analyzing Numerical Data

#### a. Histogram

A histogram is used to visualize the distribution of a numerical variable.

```python
plt.hist(df["Age"], bins=5)
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Histogram of Age')
plt.show()
```

- **Histogram**: Shows the distribution of numerical data by dividing it into bins.

#### b. Distplot

A distplot (distribution plot) combines a histogram with a kernel density estimate.

```python
sns.displot(df['Age'])
```

- **Distplot**: Provides a more detailed view of the data distribution, including a density curve.

#### c. Boxplot

A boxplot provides a summary of the distribution of a numerical variable through its quartiles.

```python
sns.boxplot(df['Age'])
plt.xlabel('Age')
plt.title('Boxplot of Age')
plt.show()
```

- **Boxplot**: Displays the median, quartiles, and outliers of the numerical data.

### 5. Descriptive Statistics

To get basic descriptive statistics for a numerical column:

```python
df['Age'].min()
df['Age'].max()
df['Age'].mean()
df['Age'].skew()
```

- **min()**: Minimum value of the column.
- **max()**: Maximum value of the column.
- **mean()**: Mean (average) of the column.
- **skew()**: Measures the asymmetry of the data distribution.
---