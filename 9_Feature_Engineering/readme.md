
---

# 1. Feature Engineering

Feature Engineering is a critical step in the machine learning pipeline that involves transforming raw data into features that better represent the underlying problem to the predictive models. The goal is to improve the performance and accuracy of machine learning models by creating new features or modifying existing ones.

<img src="https://github.com/KutbuddinKhan/Machine-Learning-Mastery/blob/main/9_Feature_Engineering/Feature%20Engineering.jpeg" alt="Feature engineering diagram" />

## What is Feature Engineering?

Feature Engineering is the process of selecting, modifying, or creating new input variables (features) from raw data to improve the performance of a machine learning model. It involves turning raw data into a format that helps a model make better predictions.

### Examples

Here are some common techniques and examples of feature engineering:

- **Transforming Data**: If you have a date column, you might extract new features like "day of the week," "month," or "year" to help the model understand patterns related to time.

- **Creating New Features**: You might combine two existing features to create a new one. For example, combining "height" and "weight" to create "Body Mass Index (BMI)" can be useful in health-related predictions.

- **Scaling**: Adjusting the scale of features, like normalizing all values between 0 and 1, ensures that no single feature dominates the model’s learning process.

### Example Workflow

<img src="https://github.com/KutbuddinKhan/Machine-Learning-Mastery/blob/main/9_Feature_Engineering/Flow%20Chart%20of%20FE.jpeg" alt="Flow chart of Feature Enginerring" />

1. **Data Collection**: Gather raw data from various sources.
2. **Feature Extraction**: Identify and extract relevant features from the raw data.
3. **Feature Creation**: Create new features that might enhance the model's performance.
4. **Feature Transformation**: Apply techniques like scaling, normalization, and encoding to transform the features into a suitable format for modeling.
5. **Feature Selection**: Choose the most important features that contribute significantly to the model’s performance.

---

# 2. Missing Values Imputation

Missing values imputation is a crucial data preprocessing step that involves filling in or replacing missing data points in a dataset. Incomplete data can lead to inaccurate or biased machine learning models, so imputing missing values helps ensure that the dataset is complete and usable for training and prediction.

## What is Missing Values Imputation?

Missing value imputation is the process of estimating and filling in missing data points in a dataset. When data points are missing, it can cause issues for machine learning algorithms that require complete datasets to function correctly. Imputation techniques "guess" or estimate the missing values to make the dataset whole again.

<img src="https://github.com/KutbuddinKhan/Machine-Learning-Mastery/blob/main/9_Feature_Engineering/Missing%20value%20imputation.jpeg" alt="Missing value Imputation" />

### Simple Ways to Impute Missing Values

#### 1. Mean/Median Imputation

- **Mean Imputation**: Replace missing values with the average of the available data in that feature.
  
  ```python
  import pandas as pd
  from sklearn.impute import SimpleImputer
  
  # Example: Mean Imputation
  df = pd.DataFrame({'Age': [25, 30, None, 40, None]})
  imputer = SimpleImputer(strategy='mean')
  df['Age'] = imputer.fit_transform(df[['Age']])
  ```

- **Median Imputation**: Replace missing values with the median value of the available data in that feature.
  
  ```python
  # Example: Median Imputation
  imputer = SimpleImputer(strategy='median')
  df['Age'] = imputer.fit_transform(df[['Age']])
  ```

- **Example**: If ages are missing, you might replace them with the average age of all other entries.

#### 2. Mode Imputation

- Replace missing values with the most frequent value (mode) in the feature.
  
  ```python
  # Example: Mode Imputation
  df = pd.DataFrame({'Gender': ['Male', 'Female', 'Female', None]})
  imputer = SimpleImputer(strategy='most_frequent')
  df['Gender'] = imputer.fit_transform(df[['Gender']])
  ```

- **Example**: For a column like "gender" with missing values, you could replace them with the most common gender.

#### 3. Forward/Backward Fill

- **Forward Fill**: Replace missing values with the last known value in the dataset.
  
  ```python
  # Example: Forward Fill
  df = pd.DataFrame({'Price': [100, None, 105, None]})
  df['Price'] = df['Price'].fillna(method='ffill')
  ```

- **Backward Fill**: Replace missing values with the next known value in the dataset.
  
  ```python
  # Example: Backward Fill
  df['Price'] = df['Price'].fillna(method='bfill')
  ```

- **Example**: In time-series data, you might fill missing values with the last known price (forward fill) or the next available price (backward fill).

#### 4. Using Algorithms

- Advanced techniques use machine learning algorithms to predict and fill in missing values based on other features in the dataset.
  
  ```python
  from sklearn.impute import KNNImputer
  
  # Example: Using KNN for imputation
  df = pd.DataFrame({'Age': [25, 30, None, 40], 'Salary': [50000, 60000, None, 80000]})
  imputer = KNNImputer(n_neighbors=2)
  df_imputed = imputer.fit_transform(df)
  ```

- **Example**: To estimate a missing salary, you could use other features like job title, years of experience, and education.

## Conclusion

Missing value imputation is a technique to handle incomplete data by making educated guesses to fill in the blanks. By applying appropriate imputation methods, you can ensure that your dataset is complete and your machine learning models can operate effectively.

---

# 3. Handling Categorical Values

Handling categorical values is an essential data preprocessing step in machine learning. Categorical data consists of categories or labels (such as animal types: Dog, Cat, Lion, etc.) that need to be converted into a numerical format for use in machine learning models. Since most models operate with numbers, translating these categories into numerical values is crucial for effective model training and prediction.

## What is Handling Categorical Values?

<img src="https://github.com/KutbuddinKhan/Machine-Learning-Mastery/blob/main/9_Feature_Engineering/Handling%20Categorical%20values.jpeg" alt="Diagram of Handling Categorical values" />

Handling categorical values involves converting data that consists of categories or labels into a numerical format that can be used by machine learning algorithms. This conversion allows models to process and analyze the data effectively. There are several methods to achieve this conversion, each with its advantages and disadvantages.

### Methods for Handling Categorical Values

#### 1. Label Encoding

- **Description**: Each unique category is assigned a unique integer. This method is straightforward but can introduce unintended ordinal relationships between categories.
  
  ```python
  from sklearn.preprocessing import LabelEncoder

  # Example: Label Encoding
  data = pd.DataFrame({'Animal': ['Dog', 'Cat', 'Lion', 'Sheep', 'Horse']})
  encoder = LabelEncoder()
  data['AnimalEncoded'] = encoder.fit_transform(data['Animal'])
  print(data)
  ```

- **Example**:
  | Animal | AnimalEncoded |
  |--------|---------------|
  | Dog    | 0             |
  | Cat    | 1             |
  | Lion   | 2             |
  | Sheep  | 3             |
  | Horse  | 4             |

  - **Downside**: Label Encoding might mislead the model into assuming an ordinal relationship (e.g., Horse is "greater" than Dog), which is not inherently true for categorical data.

#### 2. One-Hot Encoding

- **Description**: Create a new binary column for each category. Each column is marked as 1 or 0, indicating the presence of that category. This method avoids implying any order or relationship between categories.

  ```python
  import pandas as pd

  # Example: One-Hot Encoding
  data = pd.DataFrame({'Animal': ['Dog', 'Cat', 'Lion', 'Sheep', 'Horse']})
  one_hot_encoded_data = pd.get_dummies(data, columns=['Animal'])
  print(one_hot_encoded_data)
  ```

- **Example**:
  | Dog | Cat | Lion | Sheep | Horse |
  |-----|-----|------|-------|-------|
  | 1   | 0   | 0    | 0     | 0     |
  | 0   | 1   | 0    | 0     | 0     |
  | 0   | 0   | 1    | 0     | 0     |
  | 0   | 0   | 0    | 1     | 0     |
  | 0   | 0   | 0    | 0     | 1     |

  - **Advantage**: One-Hot Encoding ensures that the model does not infer any ordinal relationship between categories and treats each category independently.

## In Simple Words

Handling categorical values is like translating descriptive words (like animal names) into numbers so that a machine learning model can understand and process them. You can either give each category a unique number (Label Encoding) or convert each category into a binary column (One-Hot Encoding), depending on your needs. Each method helps the machine learn from the data without causing confusion.

---

# 4. Outlier Detection

Outlier detection is an important data analysis technique used to identify data points that deviate significantly from the majority of the data in a dataset. These unusual values, known as outliers, can be much higher or lower than the typical range of values. Outliers may indicate errors in data collection or may provide unique but valuable information.

## What is Outlier Detection?

Outlier detection involves identifying data points that differ significantly from other observations. Outliers may arise from various sources, including measurement errors or genuine anomalies. Detecting outliers is crucial for ensuring the quality of the data and for uncovering insights that might be hidden in the extreme values.

<img src="https://github.com/KutbuddinKhan/Machine-Learning-Mastery/blob/main/9_Feature_Engineering/Outliers%20Detections.jpeg" alt="Diagram of Outliers Detection" />

### Example

Consider a dataset containing the heights of different animals in meters:

- Dog: 0.5 meters
- Cat: 0.4 meters
- Sheep: 1 meter
- Horse: 1.6 meters
- Lion: 1.2 meters
- **Giraffe: 5.5 meters** (This is the outlier)

In this example, most animals have heights ranging from 0.4 to 1.6 meters. The giraffe, with a height of 5.5 meters, is significantly different from the others and is considered an outlier.

### Why It Matters

- **Data Errors**: Outliers might be due to errors such as typos or incorrect measurements. Identifying and correcting these errors ensures data quality.
- **Important Insights**: Outliers can also highlight important or rare events, such as discovering a new phenomenon or identifying an unusual case.

### How It's Done

1. **Visual Methods**: 
   - **Box Plot**: A graphical representation of data that shows the distribution, central value, and variability, making it easy to spot outliers.
   - **Scatter Plot**: Helps visualize how data points are distributed and can highlight points that fall far from the general trend.

   ```python
   import matplotlib.pyplot as plt
   import seaborn as sns
   import pandas as pd

   # Example DataFrame
   df = pd.DataFrame({'Animal': ['Dog', 'Cat', 'Sheep', 'Horse', 'Lion', 'Giraffe'],
                      'Height': [0.5, 0.4, 1.0, 1.6, 1.2, 5.5]})

   # Box Plot
   sns.boxplot(x=df['Height'])
   plt.title('Box Plot of Animal Heights')
   plt.show()
   ```

2. **Statistical Methods**:
   - **Z-Score**: Measures how many standard deviations a data point is from the mean. A high absolute z-score indicates an outlier.
   - **Interquartile Range (IQR)**: Calculates the range between the 1st quartile (Q1) and the 3rd quartile (Q3). Outliers are typically defined as data points that fall below Q1 - 1.5*IQR or above Q3 + 1.5*IQR.

   ```python
   from scipy import stats

   # Calculate Z-Scores
   df['Z-Score'] = stats.zscore(df['Height'])
   print(df)

   # Calculate IQR
   Q1 = df['Height'].quantile(0.25)
   Q3 = df['Height'].quantile(0.75)
   IQR = Q3 - Q1
   outliers = df[(df['Height'] < (Q1 - 1.5 * IQR)) | (df['Height'] > (Q3 + 1.5 * IQR))]
   print(outliers)
   ```

### In Simple Words

Outlier detection is like identifying the "odd one out" in your data. It helps you spot values that don’t fit the pattern of the rest, which could either be data entry mistakes or significant anomalies. Detecting these values ensures that the data is accurate and can reveal important insights.

---

# 5. Feature Scaling

Feature scaling is a critical data preprocessing step used to adjust the values of different features in a dataset so that they fall within a similar range. This is important because some machine learning models perform better when the data is on the same scale. Without scaling, features with larger values can dominate the model, leading to biased or ineffective learning.

## What is Feature Scaling?

Feature scaling involves transforming features to ensure they are on a comparable scale. This process helps improve the performance of machine learning models by preventing features with larger values from disproportionately influencing the results.

### Example

Consider a dataset with employee information, including age and salary:

- **Employee 1**: Age = 25 years, Salary = $50,000
- **Employee 2**: Age = 45 years, Salary = $120,000
- **Employee 3**: Age = 30 years, Salary = $80,000

In this example, ages range from 25 to 45, while salaries range from $50,000 to $120,000. Without scaling, the model might give undue importance to salary values simply because they are numerically larger.

### How to Scale

1. **Min-Max Scaling**:
   - **Description**: Rescales the data to a fixed range, typically 0 to 1.
   - **Formula**: \((\text{Value} - \text{Min}) / (\text{Max} - \text{Min})\)
   - **Example for Age**:
     - Minimum Age: 25
     - Maximum Age: 45
     - Scaled Age for Employee 1: \((25 - 25) / (45 - 25) = 0\)
     - Scaled Age for Employee 2: \((45 - 25) / (45 - 25) = 1\)
     - Scaled Age for Employee 3: \((30 - 25) / (45 - 25) = 0.25\)
   - This method makes ages fall within the range [0, 1], similar to how salaries can also be scaled.

2. **Standardization**:
   - **Description**: Centers the data around the mean with a standard deviation of 1.
   - **Formula**: \((\text{Value} - \text{Mean}) / \text{Standard Deviation}\)
   - **Use Case**: Standardization is useful when the data follows a normal distribution or when you need to compare features with different units.

### In Simple Words

Feature scaling is like resizing different items so they fit well together. By scaling features such as employee ages and salaries, you ensure that both features are on a similar level. This prevents any single feature from dominating the learning process of the model due to its larger numerical values.

## Libraries Installation

To perform feature scaling, you may need the following Python libraries:

```bash
pip install pandas scikit-learn
```

- **pandas**: For data manipulation and preprocessing.
- **scikit-learn**: For feature scaling and other machine learning tools.

## Example Code

Here's a summary of how to apply feature scaling using Python:

```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler, StandardScaler

# Example DataFrame
df = pd.DataFrame({
    'Employee': ['Employee 1', 'Employee 2', 'Employee 3'],
    'Age': [25, 45, 30],
    'Salary': [50000, 120000, 80000]
})

# Min-Max Scaling
min_max_scaler = MinMaxScaler()
df[['Age', 'Salary']] = min_max_scaler.fit_transform(df[['Age', 'Salary']])
print("Min-Max Scaled Data:")
print(df)

# Standardization
standard_scaler = StandardScaler()
df[['Age', 'Salary']] = standard_scaler.fit_transform(df[['Age', 'Salary']])
print("\nStandardized Data:")
print(df)
```

Replace the example code with your dataset and features as needed. Adjust any details according to your specific use case or preferences.

---

# 6. Feature Construction

Feature construction is the process of creating new features from existing ones to enhance the performance of a machine learning model. It involves combining, modifying, or transforming existing data columns to create a feature that might better capture important information not fully represented by the original features.

## What is Feature Construction?

Feature construction aims to create new, informative features from the existing ones. This process helps capture relationships or patterns in the data that can improve model performance.

### Example: Titanic Dataset

In the Titanic dataset, we have two features:

- **SibSp**: Number of siblings/spouses aboard the Titanic.
- **Parch**: Number of parents/children aboard the Titanic.

### Creating a New Feature: **FamilySize**

To better understand the family structure of passengers, you might create a new feature called **FamilySize**, which combines **SibSp** and **Parch**:

- **FamilySize** = **SibSp** + **Parch** + 1 (adding 1 to include the passenger themselves)

### Example Calculation

1. **Passenger 1**:
   - **SibSp**: 1
   - **Parch**: 0
   - **FamilySize** = 1 (SibSp) + 0 (Parch) + 1 = 2
   - This passenger has 1 sibling/spouse and no parents/children on board, so their family size is 2.

2. **Passenger 2**:
   - **SibSp**: 0
   - **Parch**: 2
   - **FamilySize** = 0 (SibSp) + 2 (Parch) + 1 = 3
   - This passenger has no siblings/spouses but has 2 parents/children on board, so their family size is 3.

### Why It Matters

By constructing the **FamilySize** feature, you capture information that may not be as apparent from **SibSp** and **Parch** alone. For instance, family size could be crucial in predicting survival chances, as larger families might have different dynamics compared to smaller ones or individuals traveling alone.

### In Simple Words

Feature construction is like mixing ingredients to make a new dish. In the Titanic dataset, you combine the number of siblings/spouses (**SibSp**) and the number of parents/children (**Parch**) to create a new feature called **FamilySize**. This new feature might provide better insights into relationships among passengers and improve the model's ability to predict outcomes like survival.

---

# 7. Feature Scaling

Feature scaling is the process of adjusting the range of your data so that different features contribute equally to a machine learning model. This is crucial because features with larger ranges can dominate those with smaller ranges, potentially affecting the model's performance and learning efficiency.

## What is Feature Scaling?

Feature scaling involves transforming the features in your dataset so they fall within a similar range. This ensures that each feature contributes proportionally to the model’s learning process.

### Example: MNIST Data

The MNIST dataset contains images of handwritten digits (0-9), where each image is a 28x28 pixel grayscale image. Each pixel in these images has a value ranging from 0 to 255, where 0 represents black and 255 represents white.

### Why Scaling Is Needed

- **Original Pixel Values**: In the MNIST dataset, pixel values range from 0 to 255.
- **Unscaled Values**: If these pixel values are used directly in a machine learning model, the model might place disproportionate importance on pixel values due to their larger range compared to other features.

### How to Scale

1. **Min-Max Scaling**
   - Rescales the pixel values to a range of 0 to 1.
   - **Formula**: \((\text{Pixel Value} - \text{Min}) / (\text{Max} - \text{Min})\)
   - For MNIST, where Min is 0 and Max is 255:
     - **Scaled Pixel Value** = \(\text{Pixel Value} / 255\)
   - **Example**: For a pixel value of 128:
     - **Scaled Pixel Value** = \(128 / 255 \approx 0.502\)

2. **Standardization**
   - Centers the data around the mean with a standard deviation of 1.
   - **Formula**: \((\text{Pixel Value} - \text{Mean}) / \text{Standard Deviation}\)
   - This method adjusts pixel values based on the average and variability of the pixel values across the entire dataset.

### In Simple Words

Feature scaling is like resizing all the values in your data to be on the same level so that no feature overshadows the others. For the MNIST dataset, this means adjusting pixel values from a range of 0-255 to a range of 0-1 (or another standardized range). This helps the model treat all features equally, leading to better and faster learning.

---

# 8. Feature Extraction

Feature extraction is the process of transforming raw data into a set of new features that can be more useful for a machine learning model. It involves identifying and creating the most relevant information from the original data to enhance model performance.

## What is Feature Extraction?

Feature extraction involves generating new features from the existing data to improve the effectiveness of a machine learning model. It helps in capturing the most important information from the raw data, often simplifying the dataset while retaining its essential characteristics.

### Example: Real Estate Data and PCA

Consider a real estate dataset with various features such as:

- **Size of the House** (in square feet)
- **Number of Bedrooms**
- **Number of Bathrooms**
- **Year Built**
- **Location (Neighborhood)**
- **Price**

**Principal Component Analysis (PCA)** is a popular technique for feature extraction. It helps in reducing the number of features by combining them into new, uncorrelated features called principal components. These components capture the most significant information in the data while reducing complexity.

### How PCA Works

1. **Combine Features**:
   - PCA identifies patterns in the data and creates new features (principal components) that summarize the original features. For instance, PCA might combine "Size of the House" and "Number of Bedrooms" into a new feature capturing the overall "House Value."

2. **Dimensionality Reduction**:
   - PCA reduces the number of features while preserving as much information as possible. This simplification often improves model performance and makes the dataset easier to handle.

### Example with Real Estate Data

1. **Original Features**:
   - Size of the House
   - Number of Bedrooms
   - Number of Bathrooms
   - Year Built
   - Location
   - Price

2. **Using PCA**:
   - PCA might combine "Size of the House," "Number of Bedrooms," and "Number of Bathrooms" into a new feature like "Overall Living Space," capturing the essence of these features in a single component.
   - Another principal component might combine "Year Built" and "Location" to reflect the "Age and Quality of the Neighborhood."

3. **Result**:
   - Instead of working with all six original features, you might end up with a few principal components that represent the most important aspects of the data.

### In Simple Words

Feature extraction is like summarizing a complex set of instructions into a simpler summary that still contains all the important information. For real estate data, PCA helps by creating new features from the original ones, leading to fewer, more meaningful features. This makes it easier for the model to learn and make predictions.

## Libraries Installation

To perform feature extraction using PCA, you may need the following Python libraries:

```bash
pip install pandas scikit-learn
```

- **pandas**: For data manipulation.
- **scikit-learn**: For PCA and other feature extraction methods.

## Example Code

Here's how you can apply PCA using Python:

```python
import pandas as pd
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

# Example data
data = {
    'Size of the House': [2000, 1500, 1800],
    'Number of Bedrooms': [3, 2, 4],
    'Number of Bathrooms': [2, 1, 3],
    'Year Built': [1990, 1985, 2000],
    'Location': [1, 2, 1],  # Encoded as integers for simplicity
    'Price': [500000, 400000, 600000]
}
df = pd.DataFrame(data)

# Standardize the data
scaler = StandardScaler()
scaled_data = scaler.fit_transform(df)

# Apply PCA
pca = PCA(n_components=2)  # Reduce to 2 components for example
principal_components = pca.fit_transform(scaled_data)

# Create a DataFrame with principal components
pc_df = pd.DataFrame(data=principal_components, columns=['PC1', 'PC2'])
print("Principal Components:")
print(pc_df)
```

Replace the example data with your dataset and adjust the code as needed.

---
