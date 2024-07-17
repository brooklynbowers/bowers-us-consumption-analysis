# U.S. Consumption Analysis 

This analysis outlines the exploratory data analysis section of the U.S. Consumption Analysis project. 

## Importing the data and examining the first five entries

```
df = pd.read_excel('file.xlsx')
df.head()
```

<img width="766" alt="Screenshot 2024-07-16 at 10 48 48 PM" src="https://github.com/user-attachments/assets/996ae9e5-d9d5-4044-83fb-37156b2b7b9d">

## Descriptions of the variables

𝑌  : Consumption - in Billion USD

𝑋  : Revenue (Income) - in Billion USD

𝑇  : Trend (Time) - A sequence  [1, 𝑁] 

𝑍  : Population - In capita

𝑃  : Consumer price index (Inflation)

*Note: The scales of these variables are very different, so the scales will need to be converted to a common measurement to complete the analysis.*

********** use this in a later explaination -- (1) Converting each scale to have the same lower and upper levels (2) Standardizing the variables and expressing scores at standard deviation units. (z-scores)************

## Exploratory Data Analysis

First, I will address any potential issues with data quality or format. Below, I check for missing values in the data, as well as check for null and zero values within the Population and Price Index variables.

```
# checking for missing values, so first specifying the columns to
# include in the missing value check
columns_to_check = ['Year', 'Consumption (Billion USD)', 'Revenue (Billion USD)', 'Population', 'Price Index']
*** Why not include other ones?

# now checking for missing values
missing_values = df[columns_to_check].isnull().sum().reset_index()
missing_values.columns = ['Column', 'Missing Values']
print("Missing Values:\n", tabulate(missing_values, headers='keys', tablefmt='psql'))

# counting null and zero values
data = {
    "Metric": ["Null Values", "Zero Values"],
    "Population": [df['Population'].isnull().sum(), (df['Population'] == 0).sum()],
    "Price Index": [df['Price Index'].isnull().sum(), (df['Price Index'] == 0).sum()]
}

# create a DataFrame from the data and print the results
counts_df = pd.DataFrame(data)
print(tabulate(counts_df, headers='keys', tablefmt='psql', showindex=False))
```

Next, running the descriptive statistics of the dataset.

```
# describe specific columns in the DataFrame
df_new = df[['Revenue (Billion USD)', 'Consumption (Billion USD)', 'Population', 'Price Index']]
descriptive_stats = df_new.describe()

# convert the descriptive statistics to a DataFrame and print
descriptive_stats_df = descriptive_stats.transpose()
print("Descriptive Statistics:\n", tabulate(descriptive_stats_df, headers='keys', tablefmt='psql'))
```











































































































