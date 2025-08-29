# Unsupervised-ML-Zomato-Restaurant-Clustering
Business Context

Zomato is an Indian restaurant aggregator and food delivery start-up founded by Deepinder Goyal and Pankaj Chaddah in 2008. Zomato provides information, menus and user-reviews of restaurants, and also has food delivery options from partner restaurants in select cities. India is quite famous for its diverse multi cuisine available in a large number of restaurants and hotel resorts, which is reminiscent of unity in diversity. Restaurant business in India is always evolving. More Indians are warming up to the idea of eating restaurant food whether by dining outside or getting food delivered. The growing number of restaurants in every state of India has been a motivation to inspect the data to get some insights, interesting facts and figures about the Indian food industry in each city. So, this project focuses on analysing the Zomato restaurant data for each city in India.

**Datasets**

<img width="486" height="683" alt="image" src="https://github.com/user-attachments/assets/577ea572-1485-4e4f-b26e-7d3e726e7dcd" />

<img width="486" height="683" alt="image" src="https://github.com/user-attachments/assets/5059e6ff-c8e7-47db-81cf-7cfa53aba59f" />

Project Summary:
This project involved analyzing Zomato restaurant data to segment restaurants based on customer sentiment and other features using unsupervised learning techniques. Here's a summary of the key tasks performed:

1. Data Loading and Initial Inspection:

Loaded two datasets: restaurant metadata (df) and restaurant reviews (df_1).
Performed initial checks on data types, missing values, and summary statistics for both dataframes.


2. Data Cleaning and Preprocessing:

Handling Missing Values: Addressed missing values in df ('Collections', 'Timings') and df_1 ('Reviewer', 'Review', 'Rating', 'Metadata', 'Time') by filling them with appropriate placeholders ('Unknown' for categorical, empty string for review text, and temporarily 'Unknown' for Rating before conversion). This was done to retain more data points for clustering.
Handling Duplicates: Removed duplicate rows from the df_1 DataFrame.
Data Type Conversion and Cleaning: Converted the 'Cost' column in df to numeric, removing non-digit characters. Cleaned the 'Rating' column in df_1 by replacing inconsistent entries ('Like', '-', 'Unknown') with NaN and then converting to numeric, filling resulting NaNs with the median rating.
Outlier Identification: Identified outliers in the 'Cost' column using the Interquartile Range (IQR) method, noting their presence without removing the rows to retain data.


3. Text Preprocessing for Sentiment Analysis:

Review Text Cleaning: Converted the 'Review' text in df_1 to lowercase and removed punctuation and special characters using regular expressions.
Tokenization, Stop Word Removal, and Lemmatization: Used the NLTK library to break down cleaned review text into tokens (words) using RegexpTokenizer (to avoid 'punkt_tab' issues), removed common English stop words, and applied lemmatization to reduce words to their base form. Handled NLTK resource downloads as needed.


4. Sentiment Analysis:

Applied the VADER sentiment intensity analyzer to the processed review text in df_1 to calculate a compound sentiment score for each review.
Aggregated the sentiment scores by restaurant in df_1 to obtain an average sentiment score for each restaurant, storing this in the restaurant_sentiment DataFrame.


5. Feature Engineering for Clustering:

Merged the df (restaurant metadata) and restaurant_sentiment DataFrames based on restaurant name to combine metadata with average sentiment.
Handled any remaining missing numerical values in the merged DataFrame by filling with the mean.
Used one-hot encoding to convert categorical features ('Cuisines', 'Collections') into numerical features suitable for clustering algorithms, handling multi-valued entries by splitting and creating dummy variables.
Created the final feature set (features_df) for clustering by combining the numerical features ('sentiment_score', 'Cost') and the one-hot encoded categorical features. Identified the indices of the categorical columns in features_df for use with K-Prototypes.


6. Clustering Algorithm Selection and Hyperparameter Tuning:

Selected K-Prototypes as a suitable clustering algorithm for the mixed numerical and categorical data.
Conducted hyperparameter tuning to determine the optimal number of clusters by evaluating the Calinski-Harabasz Index for a range of cluster numbers (2 to 5). Plotted the index values against the number of clusters to visualize the results.


7. Final Clustering:

Based on the Calinski-Harabasz plot and considering interpretability, selected an optimal number of clusters (initially 3, with discussion around 5 based on the metric).
Applied the K-Prototypes algorithm with the selected optimal number of clusters to the features_df to obtain the final cluster assignments for each restaurant, storing these labels in the merged_df.


8. Cluster Analysis and Interpretation:

Analyzed the characteristics of each cluster formed by the optimal clustering by examining the average sentiment score, average cost, and identifying the dominant cuisines and collections within each cluster. This helped in creating profiles for each restaurant segment.


9. Evaluation and Visualization:

Calculated the Silhouette and Calinski-Harabasz scores for the final optimal clustering, interpreting these metrics with caution due to the mixed data types. For the clustering with 3 clusters, the Silhouette Score was approximately 0.59 and the Calinski-Harabasz Index was approximately 223.36.
Generated a scatter plot visualizing the clusters based on average sentiment and average cost, with annotations highlighting the key characteristics of each cluster, to effectively present the clustering results.


Overall Usefulness: This project demonstrates how data preprocessing, sentiment analysis, and clustering can be combined to segment businesses based on customer feedback and key attributes. The identified restaurant clusters provide actionable insights for stakeholders (like Zomato and restaurant owners) to tailor marketing strategies, improve services, or develop targeted promotions for different segments of restaurants.
