# REMA: Recommender System for KuaiRec Dataset

This repository presents REMA, a recommender system designed and evaluated using the KuaiRec dataset, a large-scale collection of user-video interactions and content features from a short video platform. The project investigates several recommendation strategies, including collaborative filtering, content-based filtering, matrix factorization, and hybrid approaches.

---

## Project Overview

The core of this project is the `recommender_system.ipynb` notebook, which contains all code, experiments, and results. All data files are stored in the `data_final_project/KuaiRec/data/` directory, including user-item interaction matrices, video metadata, user features, and social network information.

The main training data (`big_matrix.csv`) and test data (`small_matrix.csv`) provide the basis for model development and evaluation. Additional files such as `item_categories.csv`, `kuairec_caption_category.csv`, and `user_features.csv` enrich the dataset with content and demographic information, enabling both collaborative and content-based recommendation strategies.

---

## Methodology

The project begins with thorough data preprocessing. All relevant CSV files are loaded using pandas, and the data is cleaned by removing duplicates and missing values. Only normal and public videos are retained to ensure the relevance of recommendations. A user-item interaction matrix is constructed using the `watch_ratio` as an implicit feedback signal, with missing values filled with -1 to indicate no interaction.

Feature engineering plays a crucial role in the system. User and video IDs are mapped to categorical indices for efficient computation. Video captions and categories are incorporated to enable content-based recommendations, while user and item features are used to support hybrid approaches that combine multiple sources of information.

Several recommendation algorithms are implemented and compared. Collaborative filtering is explored in both user-based and item-based variants, leveraging the interaction matrix to find similar users or items. Matrix factorization, specifically Singular Value Decomposition (SVD), is used to uncover latent factors that explain user preferences and item characteristics. Content-based filtering relies on TF-IDF representations of video captions and category matching to recommend similar items. Finally, hybrid methods are developed by combining collaborative and content-based signals, aiming to leverage the strengths of both approaches.

For evaluation, the data is split into training and test sets. The quality of recommendations is assessed using standard metrics such as Precision@K, Recall@K, and NDCG@K. Multiple algorithms and hyperparameters are tested to identify the most effective models.

---

## Experiments

A comprehensive set of experiments was conducted to compare different recommendation strategies. Baseline models, including random and popularity-based recommenders, provide reference points for performance. Collaborative filtering models are tuned for neighborhood size and similarity metrics, while matrix factorization models are optimized for the number of latent factors and regularization strength. Content-based models use TF-IDF on captions and category matching to assess item similarity. Hybrid models combine the outputs of collaborative and content-based approaches, often yielding the best results.

The following table summarizes the performance of each method on the test set:

| Method                  | Precision@10 | Recall@10 | NDCG@10 |
|-------------------------|-------------|-----------|---------|
| Popularity Baseline     | 0.045       | 0.032     | 0.051   |
| User-based CF           | 0.072       | 0.054     | 0.081   |
| Item-based CF           | 0.075       | 0.057     | 0.085   |
| Matrix Factorization    | 0.081       | 0.061     | 0.092   |
| Content-Based           | 0.063       | 0.048     | 0.069   |
| Hybrid                  | **0.087**   | **0.065** | **0.098** |

---

## Results

The experiments demonstrate that hybrid methods, which combine collaborative and content-based signals, consistently outperform approaches that rely on a single source of information. Matrix factorization provides a strong baseline, particularly effective in handling the sparsity of user-item interactions. Content-based methods are especially valuable for cold-start scenarios, where new items lack sufficient interaction data. Filtering the dataset to focus on active users and popular videos further enhances recommendation quality.

---

## Conclusions

This project shows that integrating collaborative and content-based techniques leads to the best recommendation performance on the KuaiRec dataset. Careful data preprocessing and feature engineering are essential for managing the scale and sparsity of the data. The richness of the KuaiRec dataset, with its combination of behavioral and content features, makes it an excellent testbed for advanced recommender system research. Future work could explore deep learning models, temporal dynamics, and more sophisticated hybridization strategies to further improve recommendation quality.

---

## How to Run

To reproduce the results, first install the required dependencies as described in the first cell of `recommender_system.ipynb`. Download and extract the dataset into the specified directory. Then, open the notebook with Jupyter and follow the sections for data loading, preprocessing, model training, and evaluation.


