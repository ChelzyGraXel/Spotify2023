# Exploratory Data Analysis on Spotify 2023 Dataset 🎧
**General Guidelines**

In this deliverable, you will perform an exploratory data analysis (EDA) on a dataset containing information about popular tracks on Most Streamed Spotify Songs 2023. This task aims to analyze, visualize, and interpret the data to extract meaningful insights.

## 💻 INTRODUCTION
What is an **_Exploratory Data Analysis (EDA)_**? It is an approach in data analysis that gives emphasis on the exploration and visualization of datasets to observe patterns, trends, and anomalies. Moreover, it is a helpful tool to understand a certain phenomenon and develop insights regarding the data given. Aside from that, it is best used for descriptive statistics, correlation analysis, group comparisons and etc. For this project, the task is to conduct an exploratory data analysis on **Most Streamed Spotify Songs 2023**.
___
#### STEP 1: Import the Pandas Library
To begin, import the Pandas Library in order to gain access to its functions.

```python
# Import the Pandas Library
import pandas as pd
```
#### STEP 2: Load the CSV file into the Data Frame
Assign the data frame to a variable named **tify**. In this particular step, I asked for help from ChatGPT since it can't load the CSV file without the additional syntax `encoding='ISO-8859-1`. According to ChatGPT, it is often used for files containing special characters.

```python
# Read CSV file
tify = pd.read_csv('spotify-2023.csv', encoding='ISO-8859-1')
```

## 🔎 OVERVIEW OF DATASET
#### STEP 3.1: Rows and Columns of the Dataset
How many rows and columns does the dataset contain? In order to output the number of columns and rows of the dataset, the following syntax was used.

```python
# Rows and columns of the dataset
rows, cols = tify.shape

# Print the results
print('Rows:', rows)
print('Columns:', cols)
```

##### OUTPUT:
The dataset contains **953 Rows** and **24 Columns**.

![image](https://github.com/user-attachments/assets/e3b6eb73-d35c-4dbf-8552-3410767cc02b)

#### STEP 3.2: Data Types of Each Column
What are the data types of each column? The syntax below was used to check the data types of each column. After using the `.dtype()` function, it returns a Series with the data type of each column in the data frame. For easier reading, the additional `.to_string()` function on the syntax code converts the Series to a string format.

```python
# Data types of each column
print('Column Name and its Data Type:')
print(tify.dtypes.to_string())
```

##### OUTPUT:
As shown in the image below, the data types of each column are indicated next to its column's name.

![image](https://github.com/user-attachments/assets/e4f5d06e-ca22-4df7-817e-94e0c89d1abe)

#### STEP 3.3: Check for Missing Values
Are there any missing values? To verify if there are columns that have missing values, the syntax below was utilized. The `.isnull()` function checks if there are any values missing in the data frame, then it returns a data frame with boolean entries. The `.sum()` counts the True values (missing values) for each column. In printing the results, the syntax `missing[missing > 0]` filters the Series and only includes columns that have more than 0 missing values. The column names are then put into a list. Finally, it prints the list of column names that have missing values.

```python
# Check if there are NaN values
missing = tify.isnull().sum()
print('\nColumns with Missing Values:', missing[missing>0].index.tolist())
```

##### OUTPUT:
The columns that have missing values are 'in_shazam_charts' and 'key'.

![image](https://github.com/user-attachments/assets/c301b316-380f-403c-bcca-ee868bcb1be8)
___
#### STEP 4: Convert Necessary Columns' Data Type
As I proceeded to code the basic descriptive statistics, I noticed that the data type for 'streams,' 'in_deezer_playlists,' and 'in_shazam_charts' is an object. In this case, the object is immutable, so it is highly recommended that it is converted first to float data type. How do we do that?

```python
# Convert necessary columns from "object" to "float"
tify['streams'] = pd.to_numeric(tify['streams'],errors='coerce')
tify['in_deezer_playlists'] = pd.to_numeric(tify['streams'],errors='coerce')
tify['in_shazam_charts'] = pd.to_numeric(tify['streams'],errors='coerce')
```

Using the function `pd.to_numeric`, it automatically converts the data type of a particular column from object to float. The `errors='coerce'` is a function in Pandas that tells the program to handle errors by converting invalid or non-convertible values to NaN (Not a Number) instead of raising an error.

## 📈 BASIC DESCRIPTIVE STATISTICS
#### STEP 5.1: Mean, Median, and Standard Deviation
What are the mean, median, and standard deviation of the streams column? In order to output the aforementioned statistical data, the following syntaxes below are used.

For the mean, I simply used the function `.mean()`, then assigned the result to a variable named **vile**.

```python
# Mean of the column 'streams'
vile = tify['streams'].mean()
```

For the median, I simply used the function `.median()`, then assigned the result to a variable named **mid**.

```python
# Median of the column 'streams'
mid = tify['streams'].median()
```

For the standard deviation, I simply used the function `.std()`, then assigned the result to a variable named **skyhigh**.

```python
# Standard deviation of the column 'streams'
skyhigh = tify['streams'].std()
```

Here's how to print the results.

```python
# Print the results
print('Mean:', vile)
print('Median:', mid)
print('Standard Deviation:', sky-high)
```

##### OUTPUT:
The calculated mean, median, and standard deviation for the column streams are 514,137,424.94, 290,530,915, and 566,856,949.04, respectively.

![image](https://github.com/user-attachments/assets/9ff1f684-f0cc-45d2-aa44-6d651cd06dcb)

___
#### STEP 5.2: Import the Matplot Library and Seaborn Library
Before we proceed, import the necessary libraries first since their functions will be used later for graphing.

```python
# Import the Matplot Library and the Seaborn Library
import matplotlib.pyplot as plt
import seaborn as sns
```
___
#### STEP 5.3: Distribution of released_year and artist_count (Graphing)
What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers? At first, I had second thoughts about whether I would use a histogram or boxplot to graph the data being asked to be observed. Then, I decided to use a boxplot because it is easier to determine the outliers in this type of graphing. As follows, there are two boxplot graphs for released_year and artist_count separately.

**Boxplot Graph of Released Year**

```python
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
```

##### OUTPUT:
As shown in the graph below, most songs are clustered around recent years (likely the 2020s) with some outliers from much earlier decades (1940s-2000s). From there, it could indicate that most of the popular songs on Spotify are newer. The outliers in earlier years (1940s, 1960s, etc.) could suggest classic songs that have remained popular or have had a resurgence in popularity.

![image](https://github.com/user-attachments/assets/04f92a63-a1ba-4d8d-b630-3454367b09ba)

**Boxplot Graph of Artist Count**

```python
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
```

##### OUTPUT:
As displayed in the graph, most popular songs are performed by only one or two artists. There are only a few outliers in the graph, which are more than two performing artists. A higher artist count indicates collaborations, which are common in hip-hop and pop genres.

![image](https://github.com/user-attachments/assets/2e8e560a-be06-4694-8e37-2c6545e26968)
___

#### STEP 6: Sort the Dataset
In the following steps of this project, there would be tasks (e.g., display the top 5 most streamed tracks) that require the dataset to be in order. In line with this, the dataset has been sorted out in descending order based on the number of streams. The following syntax below was used, and it is assigned to a variable named **stify**.

```python
# Sort the data frame in descending order based on 'streams'
stify = tify.sort_values(by='streams', ascending=False).reset_index(drop=True)
```

## 🎤 TOP PERFORMERS
#### STEP 7.1: Most Streamed Track of 2023
Which track has the highest number of streams? In order to determine the track with the highest number of streams, the syntax below was used. In my code, I specified to only output the columns: `track_name`, `artist(s)_name`, and `streams`. The output is assigned to a variable named **toptrack**.

```python
# Track which has highest number of streams
toptrack = stify[['track_name', 'artist(s)_name', 'streams']].head(1).reset_index(drop=True)
toptrack
```

##### OUTPUT:
The track that has the highest number of streams is **Blinding Lights** performed by **The Weeknd**.

![image](https://github.com/user-attachments/assets/9a202999-8319-425b-81c2-ea24e05d3fdf)

#### STEP 7.2: Top 5 Most Streamed Tracks of 2023
Display the top 5 most streamed tracks. It actually almost has the same syntax as the previous one, but this time, instead of `.head(1)`, it would be just `.head()`. This line of code automatically outputs the first five rows of the data frame. The output is assigned to a variable named **top5**. 

```python
# Top 5 most streamed tracks
top5 = stify[['track_name', 'artist(s)_name', 'streams']].head().reset_index(drop=True)
top5
```

##### OUTPUT:
The top five tracks that have the highest number of streams are displayed below. 

![image](https://github.com/user-attachments/assets/26eb5a2d-f373-44f3-89e0-df20226fc8c7)

#### STEP 7.3: Top 5 Artist with Highest Number of Tracks
Who are the top 5 most frequent artists based on the number of tracks in the dataset? Personally, this is the most challenging part of this section of the project. The code is formulated with ChatGPT's guidance. Firstly, the column `artist(s)_name` is converted to a string format using `.astype(str)` and split by a comma using `.str.split(', ')`. 

```python
# Ensure artist(s)_name column is in string format and split by ', '
stify['artist(s)_name'] = stify['artist(s)_name'].astype(str).str.split(', ')
```

After that, use the function `.explode` and `.value_counts()` to count the occurrences of the artist's name. To retrieve only the top 5, I used the function `.head()`, then it was assigned to variable `top5fr`. 

```python
# Explode the column and count occurrences
count = stify.explode('artist(s)_name')['artist(s)_name'].value_counts()
```
In printing the results, "for loop" was used to list the artists in numbered order. To itemize the artists' names, the function `.item()` was used. The number of tracks (frequency) was also listed next to the artist's name for validation.

```python
# Print the top 5 most frequent artists
top5fr = count.head(5)
print('Top 5 Most Frequent Artists based on Number of Tracks:')
for idx, (artist, frequency) in enumerate(top5fr.items()):
    print(f"{idx + 1}. {artist}: {frequency}")
```

##### OUTPUT:
The top five most frequent artists based on the number of tracks are displayed below. First on the list is Bad Bunny, with 40 tracks, followed by Taylor Swift, with 38 tracks; then The Weeknd, with 37 tracks. Lastly, SZA and Kendrick Lamar are also among the top five artists with the most tracks, with 23 number of tracks.

![image](https://github.com/user-attachments/assets/3e345e44-54c5-433e-89c5-4fe86d6da653)

## 🎼 TEMPORAL TRENDS
#### STEP 8.1: Number of Tracks Released Over Time (Per Year)
In analyzing the trends in a given dataset, graphing and visualization are a great help in generating insights regarding a phenomenon. For this section, it was asked to plot the number of tracks per year. In order to do that, I used the following syntax below.

```python
# Count the number of tracks released each year
yearly = stify['released_year'].value_counts().sort_index()

# Customize the graph
sns.set(style="darkgrid")
plt.figure(figsize=(14, 6))

# Plot using line graph
plt.plot(yearly.index, yearly.values, color='purple')

# Add title and labels
plt.title('Number of Tracks Released Yearly')
plt.xlabel('Year')
plt.ylabel('Tracks')

# Show the plot
plt.show()
```

##### OUTPUT:
In the early years, the number of tracks released was anticipatedly low, largely due to the fact that digital streaming had not yet become widely popular. Media streaming only began in the early 1990s and it took several more years for streaming platforms to gain popularity and become accessible to the general public (Volle, 2023). As internet access became more widespread starting in the 2010s, there was a noticeable rise in the number of tracks. If we analyze the graph further, the number of tracks released from 2020 to 2022 exponentially increased at its peak. This is probably influenced by the global COVID-19 pandemic, wherein a lot of artists released their music during a time when people would more likely have the time to stream at their homes during the lockdown.

![image](https://github.com/user-attachments/assets/58d6445e-d97b-4385-857c-b1b8f20b6e1c)

#### STEP 8.2: Number of Tracks Released Over Time (Per Month)
Does the number of tracks released per month follow any noticeable patterns? In order to easily navigate patterns in a given data set, data visualization is important. To plot the number of tracks released per month in a line graph, the syntax below was used.

```python
# Count the number of tracks released each month
monthly = stify['released_month'].value_counts().sort_index()

# Customize the graph
sns.set(style="darkgrid")
plt.figure(figsize=(14, 6))

# Plot using line graph
plt.plot(monthly.index, monthly.values, linestyle='-', color='purple')

# Add title and labels
plt.title('Number of Tracks Released Monthly')
plt.xlabel('Month')
plt.ylabel('Tracks')

# Show the plot
plt.xticks(monthly.index)
plt.show()
```

##### OUTPUT:
Music can sometimes be personally seasonal; preferences can depend on one’s mood, situation, or even the time of year. Just as listeners may be drawn to different styles or genres depending on their feelings, artists themselves often release music in a way that reflects their own emotions, inspirations, or even the season. The line graph below shows the number of tracks released each month of the year. It could be observed that the months of January and May have shown significant spikes in track releases. This could indicate that artists often launched new music at the beginning of the year and before the summer season. From July to August, the number of music releases decreased. The music industry could be considering that many people are on vacation, and they slow down a bit in promotional activities. As the year ends from October to November, there is a distinct increase in the number of tracks released. This might be because the holiday season is coming, and music industries are trying to make an impact before the year's end.

![image](https://github.com/user-attachments/assets/7868c7a6-38d5-4019-a7af-fc70d3cb9cbc)

## 🎸 GENRE AND MUSICAL CHARACTERISTICS
#### STEP 9.1: Correlation between Streams and Musical Attributes
To find out which attributes influence streams the most, it is necessary to do a data analysis through visualization. The following syntax was used to examine the correlation between streams and musical attributes such as bpm danceability_% and energy_%. The x-axis represents the values for the musical qualities: blue for energy_%, pink for danceability_%, and purple for BPM (beats per minute). The y-axis represents the total streams for each track in billions.

```python
# Customize the graph
sns.set(style="darkgrid")
plt.figure(figsize=(14, 6))

# Correlation between streams and musical attributes using scatter plot
plt.scatter(tify['energy_%'], tify['streams'], color='skyblue', label='Energy %')
plt.scatter(tify['danceability_%'], tify['streams'], color='pink', label='Danceability %')
plt.scatter(tify['bpm'], tify['streams'], color='plum', label='BPM')

# Add title and label
plt.title('Correlation between Streams and Musical Attributes')
plt.ylabel('Streams')

# Add legends
plt.legend(title='Musical Attributes')
plt.show()
```

##### OUTPUT:
As shown in the graph below, energy_% and danceability_% (blue and pink, respectively) tend to scatter around the lower left on the x-axis, which indicates that most of Spotify’s popular tracks have moderate energy and danceability percentages. The BPM (purple points) are more widespread on the x-axis. In line with this, most tracks with a high number of streams have a BPM below 150, and there are only a few tracks in higher BPM ranges. If we thoroughly analyze the graph, there is no strong linear relationship between the streams and music attributes. Danceability and energy seem to have a slightly more substantial influence on streams, but since the scatter of points is broad, it can not be deduced that there is a correlation between the attributes and streams.

![image](https://github.com/user-attachments/assets/dfe6a849-0bf2-47cb-9871-bb83dcd12b6a)

#### STEP 9.2: Correlation between Musical Attributes
To examine whether there is a correlation between danceability_% and energy_%, the same as valence_% and acousticness_%, the following syntaxes were used for better visualization of data. For the first graph, the danceability_% lies on the x-axis, and energy_% lies on the y-axis. For the second graph, the x-axis represents valence_%, and the y-axis represents acousticness_%.

**Scatterplot of Danceability Percent and Energy Percent**

```python
# Customize the graph
sns.set(style="darkgrid")
plt.figure(figsize=(14, 6))

# Correlation between danceability_% and energy_% using scatter plot
plt.scatter(tify['danceability_%'], tify['energy_%'], color='pink')

# Add title and label
plt.title('Correlation between Danceability and Energy')
plt.xlabel('Danceability %')
plt.ylabel('Energy %')
plt.show()
```

##### OUTPUT:
As displayed in the scatter plot below, there seems to be a slight positive correlation between the two musical attributes, namely danceability_% and energy_%. As the percentage of danceability increases, there is a tendency for the energy percentage to also rise. However, the correlation is not strong enough to draw conclusions that the danceability percentage positively influences the energy percentage. The plot suggests that higher danceability might be somewhat associated with higher energy in songs, but the correlation is likely weak to moderate.

![image](https://github.com/user-attachments/assets/93027b33-442c-4c0e-bff5-81ad9c2bece8)

**Scatterplot of Valence Percent and Acousticness Percent**

```python
# Customize the graph
sns.set(style="darkgrid")
plt.figure(figsize=(14, 6))

# Correlation between valence_% and acousticness_% using scatter plot
plt.scatter(tify['valence_%'], tify['acousticness_%'], color='plum')

# Add title and label
plt.title('Correlation between Valence and Acousticness')
plt.xlabel('Valence %')
plt.ylabel('Acousticness %')
plt.show()
```

##### OUTPUT:
As presented in the scatter plot below, there seems to be little to no linear relationship between valence_% and acousticness_%. As we observe the plot visually, the points are quite scattered across the range, and it doesn’t form any trend. In conclusion, there is a lack of a clear pattern, which implies that valence and acousticness do not have direct linear correlation.

![image](https://github.com/user-attachments/assets/ac23af04-c9fb-4d8e-af11-f3408fbcd072)

## 🍿 PLATFORM POPULARITY
#### STEP 10: Comparison of Platforms (Spotify, Apple Music, Deezer)
To navigate which platform seems to favor the most popular tracks and compare the numbers of tracks in spotify_playlists, apple_playlists, and deezer_playlists, it is necessary to plot first the data of each platforms separately. The following syntax was used.

```python
# Subplot
fig, ax=plt.subplots(1,3,figsize=(15,5))

# Spotify Plot
sns.regplot(data=tify, x='in_spotify_playlists', y='streams', color='pink', ax=ax[0])

# Apple Music Plot
sns.regplot(data=tify, x='in_apple_playlists', y='streams', color='plum', ax=ax[1])

# Deezer Plot
sns.regplot(data=tify, x='in_deezer_playlists', y='streams', color='skyblue', ax=ax[2])

# Display the Graph
plt.suptitle('Streams vs Number of Playlist')
plt.show()
```

##### OUTPUT:
To compare the different platforms, let us thoroughly analyze and understand the graphs one at a time.

🎧 Firstly, **Spotify**, which is located on the left side, its axis has the widest range, going up to 50,0000, implying that tracks appear in many Spotify playlists compared to the other platforms. Moreover, there is a positive correlation between the in_spotify_playlists and streams. 

🎧 Secondly, **Apple Music**, which is located in the middle, has an x-axis of only up to 600, indicating that there are fewer playlists overall for each track on Apple Music compared to Spotify. There is also a positive correlation, as the number of playlists increases, the streams also increase.

🎧 Lastly, **Deezer**, which is located on the right side, has an axis that ranges into the billions. The data seems heavily concentrated along the line, indicating a consistent correlation between playlist appearances and streams. However, the distribution of points is largely incomparable to other platforms.

**CONCLUSION:** In conclusion, Spotify is the platform that most likely favors popular tracks, as it has the widest distribution of tracks in playlists. Other platforms such as Apple Music appear to have a similar trend but on a smaller scale, while Deezer’s data is highly different from the two.

![image](https://github.com/user-attachments/assets/71a0ffbf-2d12-4cea-88ca-52450d9d3e8f)

## 🤓 ADVANCED ANALYSIS
#### STEP 11: Patterns (Keys and Mode)
To identify the patterns among tracks based on key or mode (Major and Minor), data visualization using boxplot was utilized. Using Seaborn, the codes presented below is how I was able to plot the data for Keys and Modes, separately. 

```python
# Subplot
fig, ax=plt.subplots(1,2,figsize=(15,5))

# Distribution of Keys
sns.boxplot(data=tify, x='key', y='streams', hue='key', palette='pastel', ax=ax[0], legend=False)
ax[0].title.set_text('Stream Distribution per Key')

# Mode (Major vs. Minor)
sns.boxplot(data=tify, x='mode', y='streams', hue='mode', palette='pastel', ax=ax[1])
ax[1].title.set_text('Stream Distribution per Mode')

# Display the Graph
plt.tight_layout()
plt.show()
```

##### OUTPUT:

**Stream Distribution per Key**

As observed in the boxplot named “Stream Distribution per Key” in the chart below, there is a wide distribution of streams across different keys. Data is somehow relatively consistent in median values and other descriptive statistics. Also, it is evident that all keys have outliers, indicating particular tracks in each key that are extremely popular. The key with the highest median is the C# compared to the other keys. This possibly implies that there is a slight preference for certain keys (e.g., C#) in popular tracks.

**Stream Distribution per Mode**

For the other boxplot in the chart, namely “Stream Distribution per Mode,” it is noticeable that tracks in the Major mode have a higher median compared to the Minor mode. It can be deduced that major-key tracks are slightly higher in popularity on average. Apart from that, it is also observed that both modes have relevant outliers which indicates that some tracks are popular regardless of their type of mode.

![image](https://github.com/user-attachments/assets/1bcb5658-3a99-4a16-8905-f27de8170e72)

#### STEP 12: Frequently Appearing Artists in Playlist or Charts
There are numerous things to consider before conducting a comparison analysis among large data such as this one. One of them is to think thoroughly about what type of chart or graph is best suited to easily visualize the data. In this case, a bar graph was utilized to easily navigate the differences between the variables being compared.

First and foremost, it is necessary to determine the artists consistently appearing in playlists or charts. I have decided to retrieve the top 10 most frequently appearing artists into a new data frame called ntify. Then, find the total number of appearances of each artist in charts and playlists of different musical platforms. After that, proceed to graphing.

**Top 10 Artists by Combined Chart Appearances (Spotify, Deezer, Apple Music)**

```python
# Create a new dataframe that has artist(s) names as rows
ntify = tify[['artist(s)_name', 'in_spotify_charts', 'in_deezer_charts', 'in_apple_charts', 
              'in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].copy()
ntify['artist'] = ntify['artist(s)_name'].str.split(', ')
ntify = ntify.explode('artist')

# Sum the chart and playlists appearances across Spotify, Deezer, and Apple Music for each artist
ntify['totalapp'] = (ntify['in_spotify_playlists'] + ntify['in_spotify_charts'] +
                     ntify['in_apple_playlists'] + ntify['in_apple_charts'] +
                     ntify['in_deezer_playlists'] + ntify['in_deezer_charts'])

# Group by artist and calculate the total appearances
chartcount = ntify.groupby('artist')['totalapp'].sum().reset_index()
chartcount = chartcount.sort_values(by='totalapp', ascending=False)

# Determine the top 10 artists based on total_chart_appearances
top10 = chartcount.head(10)

# Plot
plt.figure(figsize=(14, 6))
plt.barh(top10['artist'], top10['totalapp'], color='plum')

# Add title and labels
plt.xlabel('Total Chart Appearances Across Platforms')
plt.title('Top 10 Artists by Combined Chart Appearances (Spotify, Deezer, Apple Music)')

# Invert then show results
plt.gca().invert_yaxis()
plt.show()
```

##### OUTPUT:
There are artists consistently appearing across numerous playlists and charts, displaying their broad popularity across different music platforms and diverse genres. The music of Taylor Swift, Harry Styles, and The Weeknd focuses on the genre of pop. While Bad Bunny’s and Drake’s music are under the influence of hip-hop. In streaming platforms, these genres dominated. Apart from that, there is also an instance wherein artists who blend genres, like Bad Bunny (Latin/hip-hop) and SZA (R&B/pop) are also being acknowledged. This suggests that music coordinating different genres tends to introduce their presence in playlists and charts. In general, the aforementioned genres have consistently represented multiple charts, which concludes that there are really certain genres or artists that appear on charts as they are enjoyed by the majority of the music listeners and streamers.

![image](https://github.com/user-attachments/assets/76eb4549-e945-460a-a229-3b2d5720d86c)

___

## 🔗 REFERENCES
- **Riady, C. J.** Spotify Data 2023 - EDA and Visualizations. kaggle. Retrieved from https://kaggle.com/code/cijojidanriady/spotify-data-2023-eda-and-visualizations?fbclid=IwZXh0bgNhZW0CMTEAAR0zQsqA5ZVMO_1GnC8Klco7jNSIl4_UmSURIfw1VQaspEKErgtoiX6-i5A_aem_t6977cwnT-e7NsnJekeNAQ
- **Volle, A**. (2023, April).  Streaming Media. Britannica. Retrieved from https://www.britannica.com/technology/streaming-media 

## TOOLS

📒 **Jupyter Notebook**

It is a tool that allows a user to create documents containing code, equations, visualizations, and explanatory text. It is widely utilized in data science, machine learning, academic research, and scientific computing for data exploration, analysis, and presentation.

🧠 **ChatGPT**

It is an artificial intelligence (AI) language model that uses advanced technology to generate responses to user input's needs. Moreover, it is a helpful tool that can engage in conversations, answer questions, provide explanations, assist with creative writing, and help with a range of tasks across various domains.
