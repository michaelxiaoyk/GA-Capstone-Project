![GA logo](https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67)

General Assembly Capstone Project - Recommended Systems based on NLP and Sentiment Analysis
by Michael Xiao
Class: Data Science Immersive - 8

__Background__

3 months ago, I entered into General Assembly to pursue a Data Science course. As part of my final project, I focused my efforts on Natural Language Processing, Sentiment Analysis and Recommender Systems (RecSys). This project is a work in progress as more improvement(s) will be made over time if deemed fit.

__Disclaimers__

Basic knowledge of python and machine learning is highly recommended, lingos included. If you do not understand the above lingos mentioned, please check out these links (I find them awesome!):
1. [Natural Language Processing](https://www.analyticsvidhya.com/blog/2017/01/ultimate-guide-to-understand-implement-natural-language-processing-codes-in-python/ "NLP")
2. [VADER](https://medium.com/analytics-vidhya/simplifying-social-media-sentiment-analysis-using-vader-in-python-f9e6ec6fc52f "VADER")
3. [TextBlob](https://www.analyticsvidhya.com/blog/2018/02/natural-language-processing-for-beginners-using-textblob/ "TextBlob")
4. [Recommended System](https://www.analyticsvidhya.com/blog/2016/06/quick-guide-build-recommendation-engine-python/ "RecSys")

___Project___

Dataset: Amazon Fine Food Reviews from Kaggle
link: https://www.kaggle.com/snap/amazon-fine-food-reviews

__Executive Summary__

This project can be split into two parts: Sentiment Analysis and RecSys.
1. Sentiment Analysis
   - Initial Cleaning and EDA
   - Feature Engineering
   - Text Preprocessing with NLTK
   - VADER Sentiment Analysis
   - TextBlob Sentiment Analysis
   - Hybrid Score
   - Tackling the Cold-Start Problem

**Data Dictionary**

|Column|Description|
|------|------|
|ProductId|Specific product id from a product user bought|
|UserId|Amazon UserId|
|hybrid_score|Helpful sentiment reviews score|

__Conclusion__

We focused on using what users reviewed on Amazon products to find out if this score differs from the original 'Score' provided in our data. It turns out that the hybrid score has a 0.076272 correlation score when compared against the original 'Score' feature. This suggests that user ratings may not tally with their sentiments of the particular product. Our hybrid score also takes into account whether or not a product is deemed helpful (a fraction ranging from 0.0 to 1.0) to filter out reviews that were not helpful, especially in our analysis. Thereafter, we attempted to run our RecSys based on the hybrid_score attained.

2. RecSys
   - Surprise!
   - Matrix Factorization
   - Content-Based Filtering
   - Collaborative Filtering
   - Hybrid 

**Data Dictionaries**

|Column|Description|
|---|---|
|UserId|Amazon UserId|
|ProductId|Specific product id from a product user bought|
|hybrid_score|Helpful sentiment reviews score|
|product_name|Name of product|
|CAT1|Main category of product|
|CAT2|sub-category of product|
|CAT3|3rd sub-category of product|
|CAT4|4th sub-category of product|
|CAT5|5th sub-category of product|
|CAT6|6th sub-category of product|

Surprise! package  was used to kick off the start of our RecSys model as to compare RMSE scores for different algorithms. Furthermore, GridSearchCV on Surprise! also allows us to find the best hyper parameters to use for our chosen model. Despite not being the best model for this case, we went ahead with SVD for the purpose of matrix factorisation. Our RMSE score of 0.2120 on our test set suggests that there are room for improvement as this score is considered relatively large for our current dataset. 

The goal for Capstone 2 will be to minimise our RMSE score by adopting the Baseline Only model(best RMSE score throughout). Also, we will explore regularisation methods that may be adopted to our current SVD model, and find ways to get our RMSE scores as low as possible. As for now, we shall focus on our current model and take the best estimates whenever possible. Moving on, our SVD model helped us derive our 'm x m' and 'n x n' matrixes for our RecSys, which solves our sparsity problem. Our RecSys be sorted to two main features, Score and Product Categories, to display the ideal product(s) for the given RecSys method.

_Item Recommender_
Our item recommender focuses on the cosine similarity between products to recommend other products. The results are then sorted to only recommend products with similar categories and similar hybrid scores. Our recommender works fairly decent.

_Collaborative Filtering_
Our collaborative filtering recommender will recommend a dataframe of products given a 'UserId'. Products recommended are similar in terms of predicted scores from our SVD model and sorted to product categories. 
