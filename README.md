|<h1> Credit Card Fraudelty: A Data Mining Project </h1> <br> ![img](https://cdn-icons-png.flaticon.com/512/11094/11094299.png)  | 
| :---------: |
#
>[!IMPORTANT]
>Before running the source code on your VS Code/Jupyter/Colab, Please make sure you have all the dependencies installed by running the following command in the terminal"
> `pip install -r requirements.txt`

<hr>

You can find the dataset in [kaggle](https://www.kaggle.com/datasets/shubhamjoshi2130of/abstract-data-set-for-credit-card-fraud-detection).

<hr>

# Project Overview
This is a Data Mining project that simply detects fraud credit cards and prevent them from going any further with transactions to avoid scams.
In this repository we'll discuss 5 main points:
1. [Data Explain and Clean.](#1-data-explain-and-clean)
2. [Training data with Agglomerative Clustering method.](#2-agglomerative-clustering-method)
3. [Training data with K-Medoids method.](#3-k-medoids-clustering-method)
4. [Training data with Naive Bayes method.](#4-naive-bayes-method)
5. [Conclusion](#Conclusion)

# 1. Data Explain and Clean
## Explain
this data has 11 trainable features and 1 output.
| Feature | Description |
| - | :-: |
| Merchant_id | The id of Merchant `int` |
| Transaction date | The date of the transaction `datetime`|
| Average Amount/transaction/day | Average amount of each transaction per day `float` |
| Transaction amount | Amount deducted from the transaction `float` |
| Is declined | Did the card got declined upon that transaction? `bool`|
| Total Number of declines/day | Total number of card declines in a day. `int` |
| isForeignTransaction | Is the transaction is done through a foreign ATM or to a foreign store ? `bool` |
| isHighRiskCountry | If the origin country of the merchant or the location of transaction is considered a high risk. `bool` |
| Daily_chargeback_avg_amt | Average amount of daily chargeback. `float` |
| 6_month_avg_chbk_amt | Average amount of chargeback in past 6 months. `float` |
| 6-month_chbk_freq | Frequency of chargeback in past 6 months. `float` |
| isFradulent `desired output` | Is credit card fraud? `bool` |
## Clean
Only the `Transaction date` column had a sum of nulls of 3075 rows, the rest were 0.
+ Knowing that the total records of data are 3075 rows, we dropped this useless column.
+ The `Merchant_id` is also a useless column, so it's dropped.
+ With dropping 2 of main features, we have now 9 trainable features.

# 2. Agglomerative Clustering Method
<details><summary> <b>Algorithm Explaining</b></summary> 
The agglomerative Clustering performs a hierarchical clustering using a bottom up approach: each observation starts in its own cluster, and clusters are successively merged together. 
  It recursively merges pair of clusters of sample data; uses linkage distance.
</br></br>
 <details> <summary> <b> Hierarchical Clustering </b> </summary>
  Hierarchical clustering is a general family of clustering algorithms that build nested clusters by merging or splitting them successively. This hierarchy of clusters is represented as a tree (or dendrogram).
The root of the tree is the unique cluster that gathers all the samples, the leaves being the clusters with only one sample. </details>
</details>

![image](https://github.com/KatrineAshraf/Credit-Card-Fraudelty/assets/96535434/f0f949cc-1656-4763-86f6-992b28557781)

However its accuracy of `85%`, this method rarely detected any fraud credit cards and had many false positives (which is very dangerous) as shown in the confusion matrix below:

![image](https://github.com/KatrineAshraf/Credit-Card-Fraudelty/assets/96535434/857c0b1a-6078-4015-8f42-aa51db24a1ab)

# 3. K-Medoids Clustering Method

<details> <summary> <b>Algorithm Explaining</b></summary> K-medoids clustering is a variant of K-means that is more robust to noises and outliers. Instead of using the mean point as the center of a cluster,
K-medoids uses an actual point in the cluster to represent it. Medoid is the most centrally located object of the cluster, with minimum sum of distances to other points.
However, K-Means is not used because it is sensitive to outliers, because a mean is easily influenced by extreme values</details>

In order to cluster the points to two clusters of "Fraud" and "Not Fraud", it was disucssed to let the data be compressed from 9 learnable features to only 2 using PCA.


![image](https://github.com/KatrineAshraf/Credit-Card-Fraudelty/assets/96535434/e9496200-29ab-4edc-89e4-3a7385d7a6b2)

Although PCA has improved the accuracy from `28.98%` to `29.04%`, it wasn't good enough as it was falsely predicting fraud credit cards as not frauds and vice versa.
The sum of the true diagonal values is way less than the false ones.

![image](https://github.com/KatrineAshraf/Credit-Card-Fraudelty/assets/96535434/66f5b3c4-bcc9-44ca-a034-b6f2890d5f44)

# 4. Naive Bayes Method

<details> <summary> <b>Algorithm Explaining</b></summary> This model predicts the probability of an instance belongs to a class with a given set of feature value.
  It is a probabilistic classifier. It is because it assumes that one feature in the model is independent of existence of another feature. In other words, 
  each feature contributes to the predictions with no relation between each other. In real world, this condition satisfies rarely.
  It uses Bayes theorem in the algorithm for training and prediction </details>

  ![image](https://github.com/KatrineAshraf/Credit-Card-Fraudelty/assets/96535434/2c5adf2e-9037-4ba1-93d2-85983ac19984)

Naive Bayes was the most successful, and it had accuracy of `94.47%` with a very promising confusion matrix:

![image](https://github.com/KatrineAshraf/Credit-Card-Fraudelty/assets/96535434/04dca9a3-ca7c-4a6a-a53a-2a98d0794b33)

# Conclusion
Between Agglomerative, K-Medoids (with PCA), and Naive Bayes to learn the ability to distinguish between fraud and non-fraud credit cards. Naive Bayes was the most promising.
