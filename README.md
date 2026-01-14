# Multi-Class Model Selection using ROC and Precision-Recall Curves

### Author: Manish Nayak
### Roll No.: CE22B069

---

## 1. Objective

This project challenges the application and interpretation of **Receiver Operating Characteristic (ROC)** curves and **Precision-Recall Curves (PRC)** for model selection in a multi-class, complex classification environment. The goal is to compare a diverse set of classifiers, including those known to perform poorly, to determine the best-performing and worst-performing models for a satellite image classification task. The analysis goes beyond simple accuracy metrics to evaluate performance across different decision thresholds.

---

## 2. Problem Statement

As a machine learning scientist, the task is to classify land cover types using satellite image data. The **UCI Landsat Satellite dataset** is used, which presents a multi-class problem (6 classes) known for its high feature dimensionality and potential class overlap.

The primary goal is to perform robust model selection by comparing various classifier types using ROC and PRC analysis adapted for a multi-class setting (One-vs-Rest averaging).

---

## 3. Dataset

-   **Name**: Landsat Satellite Dataset
-   **Source**: UCI Machine Learning Repository
-   **Download Link**: [UCI Statlog (Landsat Satellite) Data Set](https://archive.ics.uci.edu/dataset/146/statlog+landsat+satellite)
-   **Citation**: Blake, C. and Merz, C.J. (1998). *UCI Repository of machine learning databases*. Irvine, CA: University of California, Department of Information and Computer Science.
-   **Description**: The dataset is a classic multi-class problem with six primary land cover classes. It is pre-split into training (`sat.trn`) and testing (`sat.tst`) sets. The data consists of 36 numerical features representing multi-spectral values.

---

## 4. Models Compared

A diverse set of classifiers was trained and evaluated to span different performance levels, from a simple baseline to high-performance ensembles.

1.  **K-Nearest Neighbors (KNN)**
2.  **Decision Tree Classifier**
3.  **Dummy Classifier (Baseline)**
4.  **Logistic Regression**
5.  **Gaussian Naive Bayes**
6.  **Support Vector Machine (SVC)**
7.  **Random Forest** *(Brownie Points Task)*
8.  **XGBoost** *(Brownie Points Task)*
9.  **Anti-Classifier** *(Brownie Points Task, to demonstrate AUC < 0.5)*

---

## 5. Analysis Pipeline

The project is structured into four main parts, following the assignment guidelines.

#### Part A: Data Preparation and Baseline Evaluation
1.  **Load and Prepare Data**: The Landsat dataset is loaded from the UCI repository. The 6 target classes are mapped to be zero-indexed.
2.  **Standardize Features**: Input features (X) are standardized using `StandardScaler` to ensure models sensitive to feature scale perform optimally.
3.  **Train Models**: An instance of each of the specified model classes is trained on the training data. For SVC, `probability=True` is set to enable probability predictions for ROC/PRC analysis.
4.  **Baseline Evaluation**: The initial performance of all models is calculated using **Overall Accuracy** and **Weighted F1-Score**.

#### Part B: ROC Analysis for Model Selection
1.  **Multi-Class ROC**: The One-vs-Rest (OvR) approach is used to generate ROC curves for the multi-class problem. The curves are then macro-averaged to produce a single representative curve for each model.
2.  **Plotting & Interpretation**: The macro-averaged ROC curves are plotted on a single graph. The model with the highest **Area Under the Curve (AUC)** is identified as the best performer under this metric. The conceptual meaning of an AUC < 0.5 is also discussed.

#### Part C: Precision-Recall Curve (PRC) Analysis
1.  **PRC Calculation**: The importance of PRC analysis, especially for datasets with class imbalance, is explained. Micro-averaged PRC curves are generated using the OvR approach.
2.  **Plotting & Interpretation**: The PRC curves are plotted, and the model with the highest **Average Precision (AP)** is identified. The behavior of the worst-performing model's PRC is analyzed to explain why its curve drops sharply.

#### Part D: Synthesis and Final Recommendation
1.  **Synthesis**: Model rankings from the F1-Score, ROC-AUC, and PRC-AP are compared. Any misalignments in rankings are explained by discussing the trade-offs between point-based metrics (like F1) and threshold-independent metrics (like AUC).
2.  **Recommendation**: Based on the comprehensive analysis, a final model is recommended for the classification task, with a full justification based on its performance across different thresholds and its balance of precision and recall.

#### Brownie Points Task
1.  **Advanced Models**: `RandomForestClassifier` and `XGBClassifier` are trained and evaluated, demonstrating their superior performance compared to the initial set of models.
2.  **AUC < 0.5 Model**: An `AntiClassifier` is created by wrapping a competent model (KNN) and inverting its probability predictions. This successfully demonstrates a classifier that performs worse than random chance, achieving an AUC score close to 0.

---

## 6. Key Findings & Results

-   The **Support Vector Classifier (SVC)** was the best-performing model among the initial six, achieving the highest Macro-averaged ROC-AUC (**0.985**) and the highest Micro-averaged PRC-AP (**0.964**). This demonstrates its robustness across all decision thresholds.
-   While KNN had a slightly higher F1-Score, its rank dropped below SVC in the more comprehensive ROC and PRC analyses, highlighting the importance of evaluating models beyond default thresholds.
-   The ensemble models, **Random Forest** and **XGBoost**, outperformed all other models, with ROC-AUC scores of **0.990**.
-   The **Dummy Classifier** served as an effective baseline, with an AUC of 0.500 (random chance) and a PRC curve near the no-skill line.
-   The **Anti-KNN Classifier** successfully demonstrated a model with performance worse than random, achieving a Macro ROC-AUC of **0.0191**.

---

## 7. How to Run

This project is contained within a single Jupyter Notebook (`assignment-7.ipynb`).

**Dependencies:**
-   Python 3.x
-   numpy
-   pandas
-   matplotlib
-   seaborn
-   scikit-learn
-   xgboost

**Instructions:**
1.  Ensure you have a Jupyter environment with the above libraries installed.
2.  Open the `assignment-7.ipynb` notebook.
3.  Run the cells sequentially from top to bottom to replicate the analysis, visualizations, and results. The notebook automatically downloads the dataset from the internet.
