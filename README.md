# Countries Categorisation by Socio-Economic and Health Factors

This Jupyter Notebook demonstrates the process of categorising countries based on socio-economic and health factors to determine their development status. The analysis is performed using the K-means clustering algorithm.

## Introduction

### Objective
The objective of this analysis is to group countries using socio-economic and health factors to determine their development status. By applying the K-means clustering algorithm, we aim to categorise countries into distinct clusters based on these factors.

### Dataset Attributes
The dataset used in this analysis contains the following attributes:

- `country`: name of the country
- `child_mort`: death of children under 5 years of age per 1000 live births
- `exports`: exports of goods and services per capita, given as a percentage of the GDP per capita
- `health`: total health spending per capita, given as a percentage of GDP per capita
- `imports`: imports of goods and services per capita, given as a percentage of the GDP per capita
- `income`: net income per person
- `inflation`: the measurement of the annual growth rate of the Total GDP
- `life_expec`: the average number of years a newborn child would live if the current mortality patterns remain the same
- `total_fer`: the number of children that would be born to each woman if the current age-fertility rates remain the same
- `gdpp`: the GDP per capita, calculated as the Total GDP divided by the total population

### Data Loading and Exploration

#### Loading the Dataset
The dataset is loaded into a pandas DataFrame using the `pd.read_csv()` function. The loaded dataset is stored in the `df` variable.

#### Checking Data Types and Counts
The `df.info()` function is used to check the data types and counts of each column in the DataFrame. This provides an overview of the column names, their corresponding data types, and the count of non-null values for each column.

#### Getting Descriptive Statistics
The `df.describe()` function is used to get descriptive statistics of the DataFrame. It provides a summary of the central tendency, dispersion, and shape of the distribution for each numeric column.

#### Identifying Missing Data
The `df.isnull().sum()` function is used to identify any missing data in the DataFrame. It returns the count of missing values for each column.

### Preprocessing and Feature Selection

#### Dropping Non-numeric Features
Non-numeric features (columns) are dropped from the DataFrame using the `df.select_dtypes()` function with the `include=[np.number]` parameter. This ensures that only numeric columns are retained for further analysis.

#### Creating a Correlation Matrix
A correlation matrix is created using the `df.corr()` function to explore the relationships between features. The correlation matrix is visualised using a heatmap from the seaborn library.

#### Exploring Features using Scatter Plots
Scatter plots are created to explore the relationships between the continuous independent features and the target variable (e.g., child mortality or GDP per capita). The `sns.scatterplot()` function from the seaborn library is used to create the scatter plots.

#### Creating a Pair Plot
A pair plot is created using the `sns.pairplot()` function from the seaborn library to visualise the relationships between all pairs of continuous independent features. The pair plot helps identify potential features for clustering based on their distributions and correlations.

### Data Scaling

#### Normalising the Data using MinMaxScaler
The data is normalised using the `MinMaxScaler` from the scikit-learn library. The `MinMaxScaler` scales the features to a specified range, typically between 0 and 1. The normalised data is stored in a new DataFrame named `df_scaled`.

### K-means Clustering

#### Selecting the Optimal Number of Clusters

##### Elbow Method
The elbow method is used to plot the within-cluster sum of squares (WSS) against the number of clusters. The elbow point in the plot suggests a good choice for the number of clusters.

##### Silhouette Score Method
The silhouette score method is used to evaluate the quality of clustering for different numbers of clusters. The silhouette score measures how well each data point fits into its assigned cluster compared to other clusters. The number of clusters with the highest silhouette score is considered optimal.

#### Fitting K-means with the Selected Number of Clusters
The K-means algorithm is fitted to the scaled dataset using the selected optimal number of clusters. The `KMeans` class from the scikit-learn library is used to initialise and fit the K-means model.

#### Counting the Number of Records in Each Cluster
The number of records in each cluster is counted using the `pd.Series(kmeans.labels_).value_counts()` function. This provides insights into the distribution of data points across the clusters.

#### Checking Model Performance with Silhouette Coefficient
The silhouette coefficient is calculated using the `silhouette_score()` function from the scikit-learn library to assess the performance of the K-means model. A higher silhouette coefficient indicates better clustering quality.

### Cluster Analysis and Visualisation

#### Adding Predicted Cluster Labels to the Original DataFrame
The predicted cluster labels obtained from the K-means model are added to the original DataFrame as a new column named 'Cluster'. This allows for further analysis and visualisation of the clustering results.

#### Visualising Clusters: Child Mortality vs GDP per Capita
A scatter plot is created to visualise the clusters based on child mortality rates and GDP per capita. The `sns.scatterplot()` function from the seaborn library is used, with the 'Cluster' column as the hue parameter to colour-code the data points based on their assigned clusters.

#### Visualising Clusters: Inflation vs GDP per Capita
Similar to the previous visualisation, a scatter plot is created to visualise the clusters based on inflation rates and GDP per capita.

### Cluster Labelling and Justification

#### Labelling Clusters based on Development Status
The clusters are labelled based on their characteristics and the development status they represent. Labels such as "Least Developed", "Developing", and "Developed" or "Low Income", "Lower-Middle Income", "Upper-Middle Income", and "High Income" can be assigned to the clusters.

#### Justifying the Assigned Labels
The assigned labels are justified based on the patterns observed in the plots and the characteristics of the countries within each cluster. Factors such as child mortality rates, GDP per capita, and inflation rates are considered when assigning the labels.

### Feature Selection Revisited

#### Correlation Analysis
A correlation analysis is performed to identify highly correlated features. The correlation matrix is computed using `df.corr()`, and highly correlated features are identified based on a specified correlation threshold.

#### Dropping Highly Correlated Features
Highly correlated features are dropped from the dataset to reduce redundancy and improve the clustering performance. The decision to drop specific features is based on domain knowledge and the specific context of the problem.

#### Updating the Clustering Process with Selected Features
The clustering process is updated using the selected features after dropping the highly correlated ones. The K-means algorithm is applied to the updated dataset, and the resulting clusters are visualised.

### Custom Visualisation Function

#### Defining the `scatter_Kmeans` Function
A custom function named `scatter_Kmeans` is defined to visualise the clusters using scatter plots. The function takes the input data, the number of clusters, and a random seed as parameters. It performs K-means clustering, assigns colours to each cluster, and plots the data points and cluster centres.

#### Visualising Clusters using the Custom Function
The `scatter_Kmeans` function is used to visualise the clusters for different combinations of features, such as child mortality vs GDP per capita and inflation vs GDP per capita.

### Error Handling and Troubleshooting

#### Resolving Key Errors
Key errors that occur when accessing columns that do not exist in the DataFrame are resolved by ensuring that the specified column names match the actual column names in the DataFrame.

#### Handling Index Errors
Index errors that occur when the number of cluster labels exceeds the available labels in the labels list are resolved by dynamically generating the cluster labels based on the number of clusters.

## Conclusion

### Interpreting the Clustering Results
The clustering results provide insights into the grouping of countries based on their socio-economic and health factors. The assigned labels and the characteristics of each cluster can be interpreted to understand the development status of the countries.

### Considerations and Limitations
It is important to consider the limitations and assumptions of the K-means algorithm when interpreting the results. The clustering is based on the selected features and may not capture all the nuances and complexities of the development status of countries. Additional factors and domain knowledge should be taken into account when making conclusions.
