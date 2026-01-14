# DA5401 Assignment 6: Imputation via Regression for Missing Data
### Name: Manish Nayak
### Roll No.: CE22B069

## 1. Objective

This project explores various techniques for handling missing data in a real-world dataset. It applies and compares simple imputation, linear regression imputation, and non-linear regression imputation. The effectiveness of each method is measured by training a logistic regression classifier on the resulting datasets and evaluating its performance in a credit risk assessment task.

## 2. Problem Statement

As a machine learning engineer on a credit risk assessment project, the task is to handle missing values within the **UCI Credit Card Default Clients Dataset**. The presence of missing data prevents the direct application of many classification algorithms. This project implements three distinct imputation strategies and a baseline listwise deletion method, then uses the cleaned datasets to train and evaluate a classification model to predict credit card payment defaults. The goal is to demonstrate how the choice of imputation technique can impact final model performance.

---

## 3. Methodology

The project is divided into three main parts: data preprocessing and imputation, model training, and comparative analysis.

### Part A: Data Preprocessing and Imputation

1.  **Data Preparation**:
    *   The UCI Credit Card dataset was loaded using pandas.
    *   To simulate a real-world scenario, Missing At Random (MAR) values were artificially introduced, replacing **5% of the values in the 'AGE' column** with `NaN`.

2.  **Imputation Strategies Implemented**:
    *   **Strategy 1: Simple Imputation (Dataset A)**: Missing values were filled with the **median** of the 'AGE' column. The median is chosen for its robustness to outliers, which are common in demographic and financial data.
    *   **Strategy 2: Linear Regression Imputation (Dataset B)**: A `LinearRegression` model was trained on the non-missing data to predict the missing 'AGE' values based on other features. This method assumes that the data is Missing At Random (MAR).
    *   **Strategy 3: Non-Linear Regression Imputation (Dataset C)**: A `KNeighborsRegressor` model was used to predict and fill the missing 'AGE' values. This approach can capture more complex, non-linear relationships between features.
    *   **Strategy 4: Listwise Deletion (Dataset D)**: As a baseline for comparison, all rows containing missing values were removed from the dataset.

### Part B: Model Training and Performance Assessment

1.  **Data Splitting**: Each of the four datasets (A, B, C, D) was split into training (80%) and testing (20%) sets.
2.  **Feature Scaling**: The features of all four datasets were standardized using `StandardScaler` to ensure that each feature contributes equally to the model's performance.
3.  **Model Training and Evaluation**: A `LogisticRegression` classifier was trained on the training set of each of the four datasets. The performance of each model was evaluated on its respective test set using a full Classification Report (Accuracy, Precision, Recall, F1-score).

---

## 4. Results and Comparative Analysis

The performance of the four models was compared, with a focus on the F1-score for the positive class (predicting a default).

### Performance Summary Table

| Method                         | Accuracy | Precision (class 1) | Recall (class 1) | F1-Score (class 1) |
| :----------------------------- | :------- | :------------------ | :--------------- | :----------------- |
| **Median Imputation**          | 0.807    | 0.685               | 0.238            | 0.353              |
| **Linear Regression Imputation** | 0.808    | 0.686               | 0.239            | 0.354              |
| **Non-Linear KNN Imputation**  | 0.808    | 0.686               | 0.239            | 0.354              |
| **Listwise Deletion**          | 0.809    | 0.707               | 0.232            | 0.349              |

### Efficacy Discussion

*   **Key Finding**: A critical observation is that **all four strategies resulted in nearly identical performance** for the final classification model. This suggests that for this specific problem (predicting default with 5% missingness in the 'AGE' feature), the choice of imputation method was not a deciding factor. This is likely because the 'AGE' feature has low predictive power compared to other variables like payment history.

*   **Listwise Deletion vs. Imputation**: While listwise deletion performed well here, it is conceptually risky. It leads to a loss of data and can introduce bias if the missingness is not completely random. Imputation methods are generally preferred as they preserve the entire dataset.

*   **Linear vs. Non-Linear Regression**: Although both methods yielded the same F1-score, non-linear regression (KNN) is conceptually more robust. It does not assume a linear relationship between features, allowing it to capture more complex patterns, which makes it a safer and more adaptable choice in general.

### Conclusion and Recommendation

Despite the identical performance metrics in this experiment, the recommended strategy for handling missing data in this scenario is **Non-Linear Regression Imputation (using KNN)**.

This recommendation is based on **conceptual soundness and risk aversion**. Non-linear imputation makes the fewest assumptions about the data's underlying structure and preserves the entire dataset, making it the most robust and professionally defensible choice for a critical application like credit risk assessment.

---

## 5. How to Run This Project

### Prerequisites

You will need Python 3 and the following libraries installed:
*   pandas
*   numpy
*   scikit-learn
*   matplotlib
*   seaborn

You can install them using pip:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
