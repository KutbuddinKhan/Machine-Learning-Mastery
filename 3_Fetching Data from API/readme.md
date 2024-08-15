
---

# Fetching and Storing Top-Rated Movies from TMDB API

This project demonstrates how to fetch data from The Movie Database (TMDB) API, process it using Pandas, and save it as a CSV file. The dataset will include information on the top-rated movies, such as movie ID, title, overview, release date, vote average, and vote count.

## Prerequisites

### Libraries Required

Before running the code, ensure that you have the following Python libraries installed:

- **pandas**: For data manipulation and analysis.
- **requests**: For making HTTP requests to the TMDB API.

You can install these libraries using `pip`:

```bash
pip install pandas requests
```

### TMDB API Key

You need a valid API key from TMDB to access their data. If you don't have an API key, sign up at [The Movie Database (TMDB)](https://www.themoviedb.org/documentation/api) and create one.

## Code Explanation

### 1. Importing Libraries

```python
import pandas as pd
import requests
```

- **pandas**: Used for creating and manipulating DataFrames.
- **requests**: Used to send HTTP requests to the TMDB API.

### 2. Fetching Data from the TMDB API

We start by sending a GET request to the TMDB API to fetch the top-rated movies:

```python
response = requests.get('https://api.themoviedb.org/3/movie/top_rated?api_key=YOUR_API_KEY&language=en-US&page=1')
response.json()['results']
```

- **response.json()**: Converts the API response into a Python dictionary.
- **response.json()['results']**: Extracts the 'results' field, which contains a list of movies.

### 3. Creating a DataFrame

We then create a DataFrame to hold the relevant information for each movie:

```python
df = pd.DataFrame(response.json()['results'])[['id', 'title', 'overview', 'release_date', 'vote_average', 'vote_count']]
df.head()
```

- **pd.DataFrame()**: Converts the list of movies into a Pandas DataFrame.
- **[['id', 'title', 'overview', 'release_date', 'vote_average', 'vote_count']]**: Selects specific columns of interest.

### 4. Looping Through Multiple Pages

The TMDB API returns a limited number of movies per page, so we loop through multiple pages to fetch all available data:

```python
df = pd.DataFrame()
for i in range(1, 479):  # Assuming there are 478 pages of results
    response = requests.get(f'https://api.themoviedb.org/3/movie/top_rated?api_key=YOUR_API_KEY&language=en-US&page={i}')
    temp_df = pd.DataFrame(response.json()['results'])[['id', 'title', 'overview', 'release_date', 'vote_average', 'vote_count']]
    df = df.append(temp_df, ignore_index=True)
```

- **for i in range(1, 479)**: Iterates through all the pages (replace `479` with the actual number of pages available).
- **df.append(temp_df, ignore_index=True)**: Appends the data from each page to the main DataFrame, ensuring that the index is reset.

### 5. Checking the DataFrame

After fetching all the data, you can check the size and structure of the DataFrame:

```python
df.shape
```

- **df.shape**: Returns the dimensions of the DataFrame (number of rows and columns).

### 6. Saving Data to CSV

Finally, save the DataFrame to a CSV file:

```python
df.to_csv("movies.csv")
```

- **df.to_csv("movies.csv")**: Exports the DataFrame to a CSV file named `movies.csv`.
---
