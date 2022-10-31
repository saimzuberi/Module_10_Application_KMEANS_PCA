# Module 10 Challenge: Crypto Clustering

![Decorative image.](Images/10-5-challenge-image.png)

## Details

I have used the starter code file to complete the tasks outlined in the Instructions. The steps for this assignment are divided into the following sections:

## Import of Data 
* i have used the code to Import the Data 
    df_market_data = pd.read_csv(
    Path("Resources/crypto_market_data.csv"),
    index_col="coin_id")

* Data has been prepared K-Means format
    scaled_data = StandardScaler().fit_transform(df_market_data)


* I have identified the Best Value for k Using the Original Data where the value of K is 4.  
    for i in k:
        k_model = KMeans(n_clusters=i, random_state=0)
        k_model.fit(df_market_data_scaled)
        inertia.append(k_model.inertia_)
        elbow_data = {"k": k, "inertia": inertia}
        df_elbow = pd.DataFrame(elbow_data)
        df_elbow.head()

* I have cluster Cryptocurrencies with K-means Using the Original Data
    predictive_market_data.hvplot.scatter(
        x="price_change_percentage_24h",
        y="price_change_percentage_7d",
        by="kmeans-segments",
        hover_cols=['coin_id']
    )


* Optimise Clusters with Principal Component Analysis and converted 7 values in the original data to 3 PCA values. 
    pca=PCA(n_components=3)
    market_data_scaled_pca = pca.fit_transform(df_market_data_scaled)
    pca.explained_variance_ratio_
### 89.5 % variance is explained in the 3 PCA variables.

* The Best Value for k Using the PCA Data which is still 4.
    df_elbow_pca.hvplot.line(
        x="k", 
        y="inertia", 
        title="Elbow Curve", 
        xticks=k
    )

* Cluster the Cryptocurrencies with K-means Using the PCA Data
    market_data_pca_predictions_df.hvplot.scatter(
        x="PCA1",
        y="PCA2",
        by="segments", 
        hover_cols=['coin_id']
    )


* Visualise and Compare the Results
    predictive_market_data.hvplot.scatter(
        x="price_change_percentage_24h",
        y="price_change_percentage_7d",
        by="kmeans-segments"
    )+market_data_pca_predictions_df.hvplot.scatter(
        x="PCA1",
        y="PCA2",
        by="segments"
        )


    df_elbow.hvplot.line(
        x="k", 
        y="inertia", 
        title="Elbow Curve", 
        xticks=k
    )+df_elbow_pca.hvplot.line(
        x="k", 
        y="inertia", 
        title="Elbow Curve", 
        xticks=k
    )
