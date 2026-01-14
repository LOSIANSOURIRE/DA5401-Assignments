# Addressing Class Imbalance in Fraud Detection

**Author:** Manish Nayak

**Roll Number:** CE22B069

## Project Objective

This project explores and evaluates different resampling strategies to handle severe class imbalance in a credit card fraud detection dataset. The primary goal is to improve the performance of a Logistic Regression classifier by creating more representative training sets using both naive and clustering-based oversampling and undersampling techniques.

## 1. Problem Statement

In the real world, datasets for fraud detection are highly imbalanced, with fraudulent transactions being extremely rare. Standard classification algorithms trained on such data are often biased towards the majority (non-fraudulent) class, leading to high overall accuracy but poor performance in identifying actual fraud. This project tackles this issue by systematically applying and comparing four different approaches to training a model:

1.  **Baseline:** Using the original, imbalanced data.
2.  **SMOTE:** Using a naive oversampling method.
3.  **Clustering-Based Oversampling (CBO):** Using a more intelligent oversampling method.
4.  **Clustering-Based Undersampling (CBU):** Using a clustering-based approach to reduce the majority class.

## 2. Dataset

The project uses the **Credit Card Fraud Detection** dataset available on Kaggle. This dataset contains transactions made by European cardholders in September 2013.

*   **Total Transactions:** 284,807
*   **Features:** 30 numerical features (28 PCA-transformed features, 'Time', and 'Amount').
*   **Class Distribution:** Highly imbalanced, with only 492 fraudulent transactions (0.173% of the total).

## 3. Methodology

The experiment is divided into three main parts:

### Part A: Data Exploration and Baseline Model
1.  **Data Loading and Analysis:** The dataset is loaded, and an initial exploratory data analysis (EDA) is performed.
2.  **Class Distribution Analysis:** The severe class imbalance is quantified and visualized.
3.  **Baseline Model (Model 1):** A Logistic Regression classifier is trained on the original, imbalanced training data. Its performance is evaluated on a stratified, imbalanced test set to establish a baseline.

### Part B: Resampling Approaches
The training data is re-engineered using three different techniques to create balanced datasets:
1.  **Naive Oversampling (Model 2: SMOTE):** The SMOTE (Synthetic Minority Over-sampling Technique) algorithm is applied to generate synthetic samples for the minority (fraudulent) class.
2.  **Clustering-Based Oversampling (Model 3: CBO):** The minority class is first grouped into clusters using K-Means. Oversampling is then performed within each cluster to ensure that the generated samples are representative of the diverse patterns in fraudulent activity.
3.  **Clustering-Based Undersampling (Model 4: CBU):** The majority class is clustered using K-Means, and the training data is undersampled by keeping only the cluster centroids, thereby preserving the distributional characteristics of the majority class while reducing its size.

### Part C: Model Comparison and Analysis
1.  **Model Training:** Three new Logistic Regression models are trained on the three balanced datasets.
2.  **Evaluation:** All four models are evaluated on the **same imbalanced test set** to ensure a fair comparison. Performance is measured using metrics robust to imbalance: **Precision, Recall, and F1-Score** for the fraudulent class.
3.  **Conclusion:** The performance of all models is compared to determine the most effective strategy and provide a final recommendation.

## 4. Results

The performance of the four models on the minority (fraudulent) class is summarized below:

| Model                       | Precision | Recall   | F1-Score |
| --------------------------- | --------- | -------- | -------- |
| **Model 1: Baseline**       | **0.8289**| 0.6429   | **0.7241**|
| Model 2: SMOTE              | 0.0581    | **0.9184**| 0.1094   |
| Model 3: CBO                | 0.0612    | 0.7241   | 0.1147   |
| Model 4: CBU                | 0.0282    | 0.8878   | 0.0547   |

## 5. Conclusion and Recommendations

While the resampling techniques (SMOTE, CBO, CBU) successfully increased the model's ability to detect fraud (high Recall), they did so at the cost of a catastrophic drop in Precision. This resulted in an unmanageably high number of false positives, rendering these models impractical for real-world deployment.

The **Baseline Model**, despite having a lower Recall, demonstrated a far superior balance between Precision and Recall, as reflected by its high F1-Score. Its high precision ensures that when an alert is raised, it is highly likely to be a genuine case of fraud.

**Recommendation:** The company should adopt the **Baseline Model** . While it fails to catch every fraudulent transaction, its alerts are reliable and actionable, which is crucial for operational efficiency and customer satisfaction.

## How to Run the Notebook

1.  **Clone the repository:**
    ```
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Launch Jupyter Notebook:**
    ```
    jupyter notebook da5401-a3-addressing-class-imbalance.ipynb
    ```

3.  **Run all cells:**
    Execute the cells in order from top to bottom. The notebook will load the data from the `/kaggle/input/` directory, perform the analysis, train the models, and generate all visualizations and results.

## Dependencies

*   pandas
*   numpy
*   matplotlib
*   seaborn
*   scikit-learn
*   imbalanced-learn
