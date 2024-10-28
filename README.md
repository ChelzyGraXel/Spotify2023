# Exploratory Data Analysis on Spotify 2023 Dataset
In this deliverable, you will perform an exploratory data analysis (EDA) on a dataset containing information about popular tracks on Most Streamed Spotify Songs 2023. This task aims to analyze, visualize, and interpret the data to extract meaningful insights.

## INTRODUCTION
What is an **_Exploratory Data Analysis (EDA)_**? It is an approach in data analysis that gives emphasis on exploration and visualization of datasets to observe patterns, trends, and anomalies. Moreover, it is a helpful tool to understand a certain phenomenon and develop insights regarding the data given. Aside from that, it is best used for descriptive statistics, correlation analysis, group comparisons and etc. For this project, the task is to conduct an exploratory data analysis on **Most Streamed Spotify Songs 2023**.

#### STEP 1: Import the Pandas Library
To begin, import the Pandas library in order to gain access to its functions.

    # Import the Pandas Library
    import pandas as pd

#### STEP 2: Load the csv File into the Data Frame
Assign the dataframe to a variable named "tify". In this particular step, I asked help from ChatGPT since it can't load the csv file without the additional syntax 'encoding='ISO-8859-1'. According to ChatGPT, it is often used for files containing special characters.

    # Read csv file
    tify = pd.read_csv('spotify-2023.csv', encoding='ISO-8859-1')

### OVERVIEW OF DATASET
#### STEP 3.1: Rows and Columns of the Dataset
How many rows and columns does the dataset contain? In order to output the number of columns and rows of the dataset, the following syntax was used:

    # Rows and columns of the dataset
    rows, cols = tify.shape

    # Print the results
    print('Rows:', rows)
    print('Columns:', cols)

#### STEP 3.2: Data Types of Each Column
What are the data types of each column? To check the data types of each column, the presented syntax below was used. After using the _.dtype( )_ function, it returns a Series with the data type of each column in the dataframe. For easier reading, the additional _.to_string( )_ function on the syntax code converts the Series to a string format.
   
    # Data types of each column
    print('Column Name and its Data Type:')
    print(tify.dtypes.to_string())

#### STEP 3.3: Check for Missing Values
Are there any missing values? To verify if there are columns that has missing values, the syntax below was utilized. The _.isnull( )_ function checks if there are any values missing in the dataframe, then it returns a dataframe with boolean entries. The _.sum( )_ counts the True values (missing values) for each column. In printing the results, the syntax _missing[missing > 0]_ filters the Series and only include columns that have more than 0 missing values. The column names are then put into a list. Finally, it prints the list of column names that have missing values.

    # Check if there are NaN values
    missing = tify.isnull().sum()
    print('\nColumns with Missing Values:', missing[missing>0].index.tolist())
    
