
---

# EDA using Bivariate and Multivariate Analysis

This guide provides an overview of how to perform Exploratory Data Analysis (EDA) using bivariate and multivariate analysis with the help of the Pandas and Seaborn libraries. The examples include scatter plots, bar plots, box plots, and more. Below, you'll find detailed explanations of each step and the functions used.

## Bivariate Analysis
Bivariate analysis involves analyzing the relationship between two variables. It helps in understanding the association, correlation, or dependence between variables. Examples include scatter plots (for numerical-numerical relationships), bar plots (for numerical-categorical relationships), and heatmaps (for categorical-categorical relationships).

## Multivariate Analysis
Multivariate analysis involves analyzing more than two variables simultaneously. This type of analysis is useful for understanding complex relationships, interactions, and patterns in the data. Examples include pair plots, cluster maps, and 3D scatter plots

## Prerequisites

Before running the code, ensure that you have the required libraries installed. You can install them using pip:

```bash
pip install pandas seaborn matplotlib
```

## Loading Datasets

We are using several datasets for the analysis:

- **Tips**: A built-in Seaborn dataset used to analyze restaurant tips.
- **Titanic**: A dataset containing information about Titanic passengers.
- **Flights**: A built-in Seaborn dataset containing information about flight passengers.
- **Iris**: A built-in Seaborn dataset used for studying the Iris flower species.

### Code:

```python
import pandas as pd
import seaborn as sns

# Load datasets
tips = sns.load_dataset('tips')
titanic = pd.read_csv("F:/100_ML/6_EDA_Univariate/train.csv")
flights = sns.load_dataset('flights')
iris = sns.load_dataset("iris")

# Display the first few rows of each dataset
print(tips.head(2))
print(titanic.head(2))
print(flights.head(2))
print(iris.head(2))
```

## 1. Scatterplot (Numerical - Numerical)

The scatterplot is used to show the relationship between two numerical variables. We can also add more dimensions to the plot by using different markers for categorical data.

### Code:

```python
sns.scatterplot(
    x="total_bill",
    y="tip",
    hue="sex",
    style="smoker",
    size="size",
    data=tips,
)
```

### Explanation:

- **`x`**: The variable on the x-axis (numerical).
- **`y`**: The variable on the y-axis (numerical).
- **`hue`**: A variable that defines different colors for different categories.
- **`style`**: Different markers for different categories.
- **`size`**: Defines the size of the markers.
- **`data`**: The dataset being used.

## 2. Bar Plot (Numerical - Categorical)

The bar plot is used to compare a numerical variable across different categories.

### Code:

```python
sns.barplot(
    x="Pclass",
    y="Age",
    hue="Sex",
    data=titanic,
)
```

### Explanation:

- **`x`**: The categorical variable on the x-axis.
- **`y`**: The numerical variable on the y-axis.
- **`hue`**: A variable to separate bars within each category.
- **`data`**: The dataset being used.

## 3. Box Plot (Numerical - Categorical)

A box plot is used to display the distribution of data and identify outliers.

### Code:

```python
sns.boxplot(
    x="Sex",
    y="Age",
    data=titanic,
    hue="Survived"
)
```

### Explanation:

- **`x`**: The categorical variable on the x-axis.
- **`y`**: The numerical variable on the y-axis.
- **`hue`**: Used to separate box plots within each category.
- **`data`**: The dataset being used.

## 4. Dist Plot (Numerical - Categorical)

The dist plot (distribution plot) shows the distribution of a numerical variable.

### Code:

```python
sns.displot(
    titanic[titanic["Survived"] == 0]["Age"],
    kind="kde",
    height=5,
    aspect=1.5 
)

sns.displot(
    titanic[titanic["Survived"] == 1]["Age"],
    kind="kde",
    height=5, 
    aspect=1.5 
)
```

### Explanation:

- **`kind`**: Specifies the type of plot, here `kde` stands for Kernel Density Estimate.
- **`height`**: Height of the plot.
- **`aspect`**: Aspect ratio of the plot.

To overlay the plots:

```python
sns.kdeplot(
    titanic[titanic["Survived"] == 0]["Age"],
    label='Not Survived',
    fill=True
)
sns.kdeplot(
    titanic[titanic["Survived"] == 1]["Age"],
    label='Survived',
    fill=True
)
```

## 5. HeatMap (Categorical - Categorical)

A heatmap is used to visualize the intensity of occurrences between categorical variables.

### Code:

```python
sns.heatmap(pd.crosstab(titanic["Pclass"], titanic["Survived"]))
```

### Explanation:

- **`pd.crosstab`**: A function to compute a cross-tabulation of two (or more) factors.
- **`sns.heatmap`**: Creates a heatmap from the cross-tabulated data.

## 6. ClusterMap (Categorical - Categorical)

A clustermap is similar to a heatmap but with added hierarchical clustering to help group similar categories.

### Code:

```python
sns.clustermap(pd.crosstab(titanic["Parch"], titanic["Survived"]))
```

### Explanation:

- **`sns.clustermap`**: A heatmap with hierarchical clustering.

## 7. Pairplot (Multivariate)

Pairplot is used to plot pairwise relationships in a dataset.

### Code:

```python
sns.pairplot(iris, hue="species")
```

### Explanation:

- **`hue`**: Adds color to distinguish between categories in the dataset.

## 8. Lineplot (Numerical - Numerical)

Line plots are used to show trends over time or continuous variables.

### Code:

```python
new = flights.groupby('year').sum().reset_index()
sns.lineplot(
    x="year",
    y="passengers",
    data=new
)
```

### Explanation:

- **`x`**: The variable on the x-axis (usually time).
- **`y`**: The numerical variable on the y-axis.
- **`data`**: The dataset being used.

### Additional Heatmap and ClusterMap for Lineplot:

```python
sns.heatmap(
    flights.pivot_table(
        values="passengers",
        index="month",
        columns="year"
    )
)

sns.clustermap(
    flights.pivot_table(
        values="passengers",
        index="month",
        columns="year"
    )
)
```

### Explanation:

- **`pivot_table`**: A pandas function to reshape data into a table format.
--- 