
# ASSIGNMENT 4: GMM-Based Synthetic Sampling for Imbalanced Data
**Author:** Manish Nayak  
**Roll No.:** CE22B069  
**Course:** DA5401 

## Project Overview

This project tackles the critical issue of class imbalance in machine learning, specifically within the context of **Credit Card Fraud Detection**. Given a dataset where fraudulent transactions are extremely rare (approximately 0.172% of the total), standard classification models often fail to learn the patterns of the minority class, leading to poor fraud detection rates.

The objective of this assignment is to implement and evaluate a sophisticated, model-based oversampling technique using a **Gaussian Mixture Model (GMM)**. By learning the underlying distribution of the fraudulent data, a GMM can be used as a generative model to create high-quality synthetic samples. This helps to create a balanced training set, allowing a classifier to better learn the nuances of the minority (fraudulent) class.

The effectiveness of this GMM-based approach is compared against a baseline Logistic Regression model trained on the original, imbalanced data.

### Dataset

The dataset used is the **Credit Card Fraud Detection** dataset, available on [Kaggle](https://www.kaggle.com/mlg-ulb/creditcardfraud). It contains transactions made by European cardholders in September 2013. The dataset is highly imbalanced, with 492 frauds out of 284,807 transactions.

## Methodology

The project is structured into three main parts:

### Part A: Data Analysis and Baseline Model

1.  **Data Preprocessing and Analysis:**
    *   The dataset was loaded and analyzed, confirming the severe class imbalance.
    *   The `Time` and `Amount` features were scaled using `StandardScaler` to ensure all features are on a comparable scale.
    *   The data was split into an 80% training set and a 20% test set using stratified sampling to maintain the original class distribution in both sets.

2.  **Baseline Model:**
    *   A baseline **Logistic Regression** classifier was trained on the original, imbalanced training data.
    *   **Evaluation:** The baseline model demonstrated a high precision (0.74) but a low recall (0.65) for the fraudulent class. This highlights the problem of imbalanced data: the model is conservative and misses a significant portion of fraudulent transactions.

### Part B: GMM Implementation and Synthetic Sampling

1.  **Theoretical Foundation:**
    *   A detailed explanation of the fundamental differences between GMM-based sampling and SMOTE is provided. GMM is a generative, distribution-based approach, whereas SMOTE is a simpler, interpolation-based method.
    *   The theoretical advantages of GMM are discussed, particularly its ability to model complex, multi-modal distributions and capture feature correlations, making it superior for generating realistic synthetic data.

2.  **GMM Hyperparameter Tuning:**
    *   To determine the optimal number of components (`k`) for the GMM, both the **Akaike Information Criterion (AIC)** and the **Bayesian Information Criterion (BIC)** were used.
    *   The analysis suggested an optimal `k` of 43 for AIC (favoring model complexity for predictive performance) and 20 for BIC (favoring model simplicity). Both were used in subsequent steps for comparison.

3.  **Data Generation Strategies:**
    Two data rebalancing strategies were implemented:
    *   **Full GMM Oversampling:** Synthetic fraudulent samples were generated to create a 1:1 balance between the majority and minority classes in the training set.
    *   **Hybrid CBU + GMM Method:** A hybrid approach where the majority class was first undersampled using **Clustering-Based Undersampling (CBU)** with K-Means. GMM was then used to oversample the minority class to match the size of the new, smaller majority class.

### Part C: Performance Evaluation and Conclusion

1.  **Model Training and Evaluation:**
    *   Four new Logistic Regression models were trained on the four new balanced datasets (one for each sampling strategy combined with each `k` value from AIC/BIC).
    *   All models were evaluated on the original, imbalanced test set to ensure a fair comparison.

2.  **Results and Comparative Analysis:**
    *   **Impact:** All GMM-based techniques dramatically improved the **Recall** for the fraudulent class to **0.91**, successfully solving the issue of missed detections.
    *   **Trade-off:** This came at the cost of a catastrophic drop in **Precision** (as low as 0.03), meaning the models produced a very high number of false positives. The F1-scores were consequently very low, indicating poor overall performance.

    The detailed results are summarized in the table below:

| Model                      | Precision | Recall   | F1-score |
| -------------------------- | --------- | -------- | -------- |
| Baseline                   | 0.738     | 0.649    | 0.691    |
| GMM Oversampling (AIC)     | 0.084     | 0.908    | 0.154    |
| GMM Oversampling (BIC)     | 0.069     | 0.908    | 0.129    |
| CBU + GMM Hybrid (AIC)     | 0.032     | 0.908    | 0.062    |
| CBU + GMM Hybrid (BIC)     | 0.034     | 0.908    | 0.066    |

## Final Recommendation and Conclusion

**GMM is a theoretically sound and powerful technique for synthetic data generation, but its application requires careful tuning to avoid overfitting the generative model itself.**

While the method was highly effective at increasing the fraud detection rate (Recall), the extremely poor Precision suggests that the synthetic data generated was not of sufficient quality. The root cause was identified as **overfitting the Gaussian Mixture Model**. For a small minority class of only 394 samples, the high number of components suggested by AIC (43) and BIC (20) meant the GMM likely modeled random noise rather than the true underlying signal. This "noisy" synthetic data then led to a poor-performing final classifier that could not effectively distinguish between true fraud and legitimate transactions near the decision boundary.

Therefore, the final recommendation is not to discard the GMM method but to refine its implementation. Future work should focus on:
*   **Constraining the complexity of the GMM** by limiting the search space for `k` to a more reasonable range.
*   **Applying regularization** to the GMM to prevent it from fitting too closely to the small minority sample.

This project serves as a practical demonstration that the quality of synthetic data is paramount, and an over-complex generative model can be just as detrimental as the original class imbalance problem.

---
