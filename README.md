## Project Description
Unsupervised learning is a powerful branch of machine learning that aims to uncover patterns, structures, and relationships within datasets without the need for explicit labels or target values. The main objective of this project is to explore, evaluate and discover valuable insights, by leveraging the power of unsupervised learning to predict if cryptocurrencies are affected by 24-hour or 7-day price changes.

<img width="350" src="https://github.com/Jayplect/CryptoClustering/assets/107348074/789cfd4b-3156-401a-823f-77feb12da371">

## Dependencies used

![SkLearn](https://img.shields.io/badge/scikit_learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)

## Methodology
### Data Collection and Preprocessing: 
The datasets used for analysis was provided by edX Boot Camps LLC, and is intended for educational purposes only. To ensure the data quality and representativeness, I performed some basic preprocessing steps such as data cleaning, feature selection ("price_change_percentage_24h" and "price_change_percentage_7d"), normalization, and checking for missing values. I utilized the `StandardScaler()` module from scikit-learn to normalize the data from the CSV file.

### Clustering Techniques: 
I implemented the elbow method to find the best value for k using the original scaled dataFrame. From the elbow curve above (Fig 1), 4 seems to be the best number of centroids to use in the kMeans clustering algorithm.

- Fig 1: Elbow curve for brute forced Kmeans on Original Scaled dataset

![elbow_curve_orig_data](https://github.com/Jayplect/CryptoClustering/assets/107348074/f8ea8450-dbd9-4498-83be-7960074d0c9d)

With the Kmeans identified above, I then clustered the cryptocurrencies by fitting the K-means model using the original scaled dataframe after which I predicted the clusters to group the cryptocurrencies again, using the original scaled dataframe. I then created a scatter plot(Fig 2) using `hvPlot` with the seleted features "price_change_percentage_24h" and "price_change_percentage_7d".
The color represents the labels found using K-means. The "coin_id" column was added in the hover_cols parameter to identify the cryptocurrency represented by each data point.

- Fig 2: Scatter plot of Original Scaled data

![scatterplot_orig_data](https://github.com/Jayplect/CryptoClustering/assets/107348074/519744b4-2bcb-4813-bce1-d997f57f2b4e)

### Dimensionality Reduction:
In this phase, I implemented dimensionality reduction technique to reduce the features to three principal components. I also retrieve the explained variance to determine how much information can be attributed to each principal component. _The total explained variance of the three principal components is 89.5%. This means that although we reduced the dimension of the scaled data to 3 but only lost the ability to explain 10.5% of the variance in the dataset_. Using the elbow method once again, I obsereved the best Value for k (Fig 3) using the PCA data. The elbow curve for the PCA dimension redution data again shows a best k-value of 4. This is perhaps more pronounced compared to the best predicted k-value in the original dataset.

- Fig 3: Elbow curve for PCA data

![elbow_curve_pca](https://github.com/Jayplect/CryptoClustering/assets/107348074/a2f0a8b0-ca16-4286-a2e4-7615a44e5b62)

Further, I clustered the cryptocurrencies with K-means using the PCA data by fitting the Kmeans model and predicting the clusters to group the cryptocurrencies using the PCA data. A scatter plot of the three reduced PCAs(Fig 4) shows a clear distinction amongst the clusters. However, we do not know which of the columns are present in each of the PCAs. As revealed from the correlations (Table 1), no linear relationships exists amongst these PCAs. I then inputed the predicted clusters from the PCA reduced dimension prediction into the original scaled data and repeated the scatter plot graphing with the new cluster (Fig. 5).

- Table 1: Correlation amongst the three PCAs

<img width="500" alt="image" src="https://github.com/Jayplect/CryptoClustering/assets/107348074/0c8d75f6-9d13-4217-8a47-98db46ed3000">

- Fig 4: Scatter plot of the three PCAs

![image](https://github.com/Jayplect/CryptoClustering/assets/107348074/025d0ea8-200d-4615-a451-710bd10d0999)

As expected, the PCA scatter plot strengthens the earlier observation from the elbow curve in the original scaled dataset and the PCA transformed dataset. The best centroids were observed to be around 4 for both curves. In other words no differences were noticed when clusters are predicted from the scaled dataset nor when predicted from the reduced dimensionality.

- Fig 5: Scatter plot of features by PCA clusters

![scatterplot_pca_clusters](https://github.com/Jayplect/CryptoClustering/assets/107348074/85cd9c78-bf52-4490-9878-113674a5c320)

A scatter plot (Fig 6) similar to that made for the orginal scaled data is shown below for two of the three PCA- PCA_1 and PCA_2. However, the color of the graph points represent the labels found using K-means on the PCA data.

Fig 6: Scatter plot of PC1 and PC2 by PCA clusters

![scatterplot_pc1_pc2](https://github.com/Jayplect/CryptoClustering/assets/107348074/d26de6e8-13e5-4c4b-bfae-46f7e27ec08d)

## Conclusion
After visually analyzing the cluster analysis results (i.e., between PC1 and PC2 versus the original scaled dataset), we can conclude that reducing the dimension of the data to 3 PCA provides distinct clusters that may be relied upon to interpret the differences between the crypto price change.

