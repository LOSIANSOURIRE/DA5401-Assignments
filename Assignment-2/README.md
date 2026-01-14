
# DA5401: Assignment 2 - Dimensionality Reduction with PCA on the Mushroom Dataset

- **Student Name:** Manish Nayak
- **Roll Number:** CE22B069

---

## 1. Project Synopsis

This project demonstrates the application of **Principal Component Analysis (PCA)** on the Mushroom Dataset to reduce dimensionality while preserving predictive information. The dataset, composed entirely of categorical features, is first preprocessed using one-hot encoding and standardization.

The core of the analysis involves using a **scree plot** to identify the optimal number of principal components required to explain 95% of the data's variance. The transformed data is then visualized to reveal the inherent class separability in the new, reduced feature space.

Finally, the effectiveness of PCA is rigorously evaluated by comparing the performance of a **Logistic Regression classifier**. One model is trained on the full, high-dimensional feature set, and a second is trained on the reduced, PCA-transformed feature set. The results show that dimensionality can be reduced by nearly 50% with a negligible impact on classification accuracy, highlighting the power of PCA in creating more efficient and robust models.

---

## 2. Submission File Structure

The submission is contained within a single directory with the following structure:

```
/submission/
├── 📜 pca-analysis-on-mushroom-dataset.ipynb
└── 📄 README.md
```

- **`pca-analysis-on-mushroom-dataset.ipynb`**: This is the primary submission file. It is a self-contained Jupyter Notebook containing all the Python code, markdown explanations, visualizations, and a complete narrative of the analysis from start to finish.
- **`README.md`**: This documentation file, providing a high-level overview, workflow summary, and instructions for evaluation.

---

## 3. Methodology & Workflow Summary

The notebook is structured into three main parts, following the assignment guidelines:

### Part A: Exploratory Data Analysis & Preprocessing

1.  **Dataset Loading:** The Mushroom dataset is loaded using `pandas`.
2.  **One-Hot Encoding:** All 22 categorical features are converted into 117 binary (0/1) features. This is a crucial step to transform the non-numeric data into a format suitable for the mathematical operations of PCA.
3.  **Standardization:** The resulting 117-dimensional dataset is standardized using `StandardScaler`. This ensures each feature contributes equally to the analysis by scaling them to have a mean of 0 and a standard deviation of 1, preventing features with higher variance (due to frequency) from dominating the PCA algorithm.

### Part B: Principal Component Analysis (PCA)

1.  **Optimal Component Selection:** PCA is first applied to the full standardized dataset. A **scree plot** is generated to visualize the cumulative explained variance. From this plot, the optimal number of components to retain 95% of the variance is determined to be **59**.
2.  **Visualization & Analysis:**
    *   A **2D scatter plot** of the first two principal components (PC1 vs. PC2) is created. This plot immediately reveals a strong linear separability between the edible and poisonous classes.
    *   To gain deeper insight, a **pair plot** of the first five principal components is generated. This visualization confirms that while PC1 is the dominant separator, the subsequent components also contribute significantly to resolving class overlaps and revealing a more complex data structure.

### Part C: Performance Evaluation with Logistic Regression

1.  **Baseline Model:** A Logistic Regression classifier is trained and evaluated on the full, 117-dimensional standardized dataset. It achieves a perfect **accuracy of 1.0000**.
2.  **PCA-Transformed Model:** The data is transformed using the 59 optimal principal components. A new Logistic Regression model is trained on this reduced dataset, achieving an **accuracy of 0.9992**.
3.  **Comparative Analysis:** The results are compared, demonstrating that PCA reduced the feature space by nearly 50% with only a negligible 0.08% drop in accuracy. This confirms that the discarded variance was primarily noise and that Logistic Regression serves as an excellent surrogate measure for the effectiveness of PCA in this context.

---

## 4. Key Findings & Conclusion

-   PCA successfully reduced the feature space by **49.6%** (from 117 to 59 features) while retaining **95%** of the original data's variance.
-   The model trained on the reduced PCA components achieved **99.92% accuracy**, proving that the dimensionality reduction did not lead to a significant loss of predictive information.
-   The primary benefit of PCA in this case was not an increase in accuracy (as the baseline was already perfect) but a significant improvement in **efficiency** (fewer features to train on) and **robustness** (by removing feature redundancy and forcing the model to learn from more general patterns).
-   Visualizations strongly confirmed the effectiveness of PCA, showing clear class separation in the new, lower-dimensional space, which explains why the classifier performed so well.

---

## 5. How to Run & Dependencies

The notebook is designed to run in a Kaggle environment or any standard Jupyter environment with the necessary libraries installed.

### Data Source

The Mushroom Classification dataset is loaded directly from the Kaggle input directory:
`/kaggle/input/mushroom-classification/mushrooms.csv`

### Required Libraries

The analysis relies on the following core Python libraries. They can be installed via `pip`.

```
pandas
numpy
matplotlib
seaborn
scikit-learn
```
