# Exploratory Data Analysis on Spotify 2023 Dataset
In this deliverable, you will perform an exploratory data analysis (EDA) on a dataset containing information about popular tracks on Most Streamed Spotify Songs 2023. This task aims to analyze, visualize, and interpret the data to extract meaningful insights.

## INTRODUCTION
What is an **_Exploratory Data Analysis (EDA)_**? It is an approach in data analysis that gives emphasis on the exploration and visualization of datasets to observe patterns, trends, and anomalies. Moreover, it is a helpful tool to understand a certain phenomenon and develop insights regarding the data given. Aside from that, it is best used for descriptive statistics, correlation analysis, group comparisons and etc. For this project, the task is to conduct an exploratory data analysis on **Most Streamed Spotify Songs 2023**.
___
#### STEP 1: Import the Pandas Library
To begin, import the Pandas Library in order to gain access to its functions.

    # Import the Pandas Library
    import pandas as pd

#### STEP 2: Load the CSV file into the Data Frame
Assign the data frame to a variable named **tify**. In this particular step, I asked for help from ChatGPT since it can't load the CSV file without the additional syntax 'encoding='ISO-8859-1'. According to ChatGPT, it is often used for files containing special characters.

    # Read CSV file
    tify = pd.read_csv('spotify-2023.csv', encoding='ISO-8859-1')

## OVERVIEW OF DATASET
#### STEP 3.1: Rows and Columns of the Dataset
How many rows and columns does the dataset contain? In order to output the number of columns and rows of the dataset, the following syntax was used:

    # Rows and columns of the dataset
    rows, cols = tify.shape

    # Print the results
    print('Rows:', rows)
    print('Columns:', cols)

##### OUTPUT:
The dataset contains **953 Rows** and **24 Columns**.
![image](https://github.com/user-attachments/assets/e3b6eb73-d35c-4dbf-8552-3410767cc02b)

#### STEP 3.2: Data Types of Each Column
What are the data types of each column? The syntax below was used to check the data types of each column. After using the _.dtype( )_ function, it returns a Series with the data type of each column in the data frame. For easier reading, the additional _.to_string( )_ function on the syntax code converts the Series to a string format.
   
    # Data types of each column
    print('Column Name and its Data Type:')
    print(tify.dtypes.to_string())

##### OUTPUT:
As shown in the image below, the data types of each column are indicated next to its column's name.
![image](https://github.com/user-attachments/assets/e4f5d06e-ca22-4df7-817e-94e0c89d1abe)

#### STEP 3.3: Check for Missing Values
Are there any missing values? To verify if there are columns that have missing values, the syntax below was utilized. The _.isnull( )_ function checks if there are any values missing in the data frame, then it returns a data frame with boolean entries. The _.sum( )_ counts the True values (missing values) for each column. In printing the results, the syntax _missing[missing > 0]_ filters the Series and only include columns that have more than 0 missing values. The column names are then put into a list. Finally, it prints the list of column names that have missing values.

    # Check if there are NaN values
    missing = tify.isnull().sum()
    print('\nColumns with Missing Values:', missing[missing>0].index.tolist())
    
##### OUTPUT:
The columns that have missing values are 'in_shazam_charts' and 'key'.
![image](https://github.com/user-attachments/assets/c301b316-380f-403c-bcca-ee868bcb1be8)
___
#### STEP 4: Convert Necessary Columns' Data Type
As I proceed to code the basic descriptive statistics, I noticed that the data type for 'streams', 'in_deezer_playlists', and 'in_shazam_charts' is object. In this case, the object is immutable, so it is highly recommended that it is converted first to float data type. How do we do that?

    # Convert necessary columns from "object" to "float"
    tify['streams'] = pd.to_numeric(tify['streams'],errors='coerce')
    tify['in_deezer_playlists'] = pd.to_numeric(tify['streams'],errors='coerce')
    tify['in_shazam_charts'] = pd.to_numeric(tify['streams'],errors='coerce')

Using the function _pd.to_numeric_, it automatically converts the data type of a particular column from object to float.

## BASIC DESCRIPTIVE STATISTICS
#### STEP 5.1: Mean, Median, and Standard Deviation
What are the mean, median, and standard deviation of the streams column? In order to output the aforementioned statistical data, the following syntaxes below are used.

For the mean, I simply used the function _mean( )_, then assigned the result to a variable named **vile**.

    # Mean of the column 'streams'
    vile = tify['streams'].mean()

For the median, I simply used the function _median( )_, then assigned the result to a variable named **mid**.

    # Median of the column 'streams'
    mid = tify['streams'].median()

For the standard deviation, I simply used the function _std( )_, then assigned the result to a variable named **skyhigh**.

    # Standard deviation of the column 'streams'
    skyhigh = tify['streams'].std()

Here's how to print the results.

    # Print the results
    print('Mean:', vile)
    print('Median:', mid)
    print('Standard Deviation:', sky-high)

##### OUTPUT:
The calculated mean, median, and standard deviation for the column streams are 514,137,424.94, 290,530,915, and 566,856,949.04, respectively.
![image](https://github.com/user-attachments/assets/9ff1f684-f0cc-45d2-aa44-6d651cd06dcb)

#### STEP 5.2: Import the Matplot Library and Seaborn Library
Before we proceed, import the necessary libraries first since their functions will be used later for graphing.

    # Import the Matplot Library and the Seaborn Library
    import matplotlib.pyplot as plt
    import seaborn as sns

#### STEP 5.3: Distribution of released_year and artist_count (Graphing)
What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

**Boxplot Graph of Released Year**

    # Customize the graph
    sns.set(style="darkgrid")
    plt.figure(figsize=(14, 6))
    
    # Boxplot of released_year using Seaborn
    sns.boxplot(data=tify, y='released_year', color='pink')
    
    # Add title and labels
    plt.title("Boxplot of Released Year")
    plt.ylabel("Released Year")
    
    # Show the plot
    plt.show()

##### OUTPUT:
![image](https://github.com/user-attachments/assets/04f92a63-a1ba-4d8d-b630-3454367b09ba)

**Boxplot Graph of Artist Count**

    # Customize the graph
    sns.set(style="darkgrid")
    plt.figure(figsize=(14, 6))
    
    # Boxplot of artist_count using Seaborn
    sns.boxplot(data=tify, y='artist_count', color='plum')
    
    # Add title and labels
    plt.title("Boxplot of Released Year")
    plt.ylabel("Artist Count")
    
    # Show the plot
    plt.show()

##### OUTPUT:
![image](https://github.com/user-attachments/assets/2e8e560a-be06-4694-8e37-2c6545e26968)
___

#### STEP 6: Sort the Dataset
In the following steps of this project, there would be tasks (e.g., display the top 5 most streamed tracks) that require the dataset to be in order. In line with this, the dataset has been sorted out in descending order based on the number of streams. The following syntax below was used, and it is assigned to a variable named **stify**.

    # Sort the data frame in descending order based on 'streams'
    stify = tify.sort_values(by='streams', ascending=False).reset_index(drop=True)

## TOP PERFORMERS
## TEMPORAL TRENDS
## GENRE AND MUSICAL CHARACTERISTICS
## PLATFORM POPULARITY
## ADVANCED ANALYSIS
