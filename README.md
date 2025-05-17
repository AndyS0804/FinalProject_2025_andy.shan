# REMA: Recommender System for KuaiRec Dataset

This repository presents REMA, a recommender system designed and evaluated using the KuaiRec dataset, a large-scale collection of user-video interactions and content features from a short video platform. The project investigates several recommendation strategies, including collaborative filtering, content-based filtering, matrix factorization, and hybrid approaches.

---


## How to Run

To reproduce the results, first install the required dependencies as described in the first cell of `recommender_system.ipynb`. Download and extract the dataset into the specified directory. Then, open the notebook with Jupyter and follow the sections for data loading, preprocessing, model training, and evaluation.

---

## Project Overview

The core of this project is the `recommender_system.ipynb` notebook, which contains all code, experiments, and results. All data files are stored in the `data_final_project/KuaiRec/data/` directory, including user-item interaction matrices, video metadata, user features, and social network information.

The main training data (`big_matrix.csv`) and test data (`small_matrix.csv`) provide the basis for model development and evaluation. Additional files such as `item_categories.csv`, `kuairec_caption_category.csv`, and `user_features.csv` enrich the dataset with content and demographic information, enabling both collaborative and content-based recommendation strategies.

---

## Methodology

The project begins with thorough data preprocessing. All relevant CSV files are loaded using pandas, and the data is cleaned by removing duplicates and missing values. Only normal and public videos are retained to ensure the relevance of recommendations. A user-item interaction matrix is constructed using the `watch_ratio` as an implicit feedback signal, with missing values filled with -1 to indicate no interaction.

Several recommendation algorithms are implemented and compared. Collaborative filtering is explored in both user-based and item-based variants, leveraging the interaction matrix to find similar users or items. Content-based filtering relies on TF-IDF representations of video captions and category matching to recommend similar items.

For evaluation, the data is split into training (big matrix) and test sets (small matrix). The quality of recommendations is assessed using standard metrics such as Precision@K, Recall@K, and NDCG@K. Multiple algorithms and hyperparameters are tested to identify the most effective models.

---

## Experiments

To assess the effectiveness of different recommendation strategies, a series of experiments were conducted. Collaborative filtering approaches were explored, both in user-based and item-based forms, with careful tuning of neighborhood size and similarity metrics to optimize results. For content-based filtering, video captions were vectorized using TF-IDF, and category information was leveraged to identify similar items. Moreover, we filtered out videos with less than 1000 interactions to ensure that the recommendations are based on popular content. And we also focused on videos with a watch ratio greater than 0.7.

The table below summarizes the performance of each method on the test set, using Precision@10, Recall@10, and NDCG@10 as evaluation metrics:

| Method                         | Precision@10 | Recall@10 | NDCG@10 |
|--------------------------------|--------------|-----------|---------|
| Content-Based                  | 0.8836       | 0.0027    | 0.9720  |
| Neural Collaborative Filtering | 0.9268       | 0.0028    | 0.9638  |


If we consider the threshold of the interactions to be 2000, the results are as follows:
| Method                         | Precision@10 | Recall@10 | NDCG@10 |
|--------------------------------|--------------|-----------|---------|
| Content-Based                  | **0.9371**   | 0.0028    | **0.9955**  |
| Neural Collaborative Filtering | 0.9332       | **0.0056**    | 0.9690  |

---

## Results

The results indicate that the content-based method outperforms the collaborative filtering approach in terms of Precision@10 and NDCG@10, while the collaborative filtering method shows a higher Recall@10. This suggests that while content-based recommendations are more precise, they may not capture as many relevant items as collaborative methods. This is likely due to the sparsity of the dataset and the nature of user interactions, where many users may not have sufficient interaction history for effective collaborative filtering. 

---

## Conclusions

In summary, combining collaborative and content-based techniques leads to the best recommendation outcomes on the KuaiRec dataset. Careful preprocessing and filtering are essential for managing the scale and sparsity of the data. The KuaiRec dataset, with its rich combination of behavioral and content features, provides an excellent foundation for developing and evaluating advanced recommender systems.

---

## Going Further

To extend this project, consider the following directions:
- Use meta-data from the KuaiRec dataset to enhance content-based recommendations. We could use video descriptions, tags, and other features to improve the quality of recommendations.
    - Investigate the impact of different hyperparameters on model performance, such as the number of neighbors in collaborative filtering or the dimensionality of TF-IDF vectors.
    - Explore the use of social network information to enhance recommendations, such as incorporating user connections or interactions with friends.
    - Consider the temporal aspect of user interactions, such as modeling the evolution of user preferences over time or incorporating time-based features into the recommendation process.
- Implement hybrid models that combine collaborative and content-based filtering in a more sophisticated manner, such as using ensemble methods or multi-task learning.
- Experiment with different evaluation metrics and thresholds to better understand the performance of the models.