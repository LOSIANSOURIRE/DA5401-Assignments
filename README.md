# DA5401 Assignment 5: Visualizing Data Veracity in Multi-Label Classification

### Name: Maish Nayak
### Roll No.: CE22B069

![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)![Libraries](https://img.shields.io/badge/Libraries-Scikit--learn%20%7C%20Pandas%20%7C%20Matplotlib-orange.svg)![Status](https://img.shields.io/badge/Status-Completed-green.svg)

This repository contains the solution for the DA5401 A5 assignment, which focuses on using non-linear dimensionality reduction techniques, **t-SNE** and **Isomap**, to visually inspect and understand data quality challenges in a multi-label biological dataset.

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Key Findings & Visualizations](#key-findings--visualizations)
  - [t-SNE Veracity Inspection](#t-sne-veracity-inspection)
  - [Isomap and the Data Manifold](#isomap-and-the-data-manifold)
- [Setup and Usage](#setup-and-usage)
  - [Prerequisites](#prerequisites)
  - [Running the Notebook](#running-the-notebook)
- [File Structure](#file-structure)

## Project Overview

The objective of this assignment is to analyze the **Yeast dataset**, which contains gene expression data, to identify common data veracity issues that challenge machine learning classifiers. These issues include:

1.  **Noisy/Ambiguous Labels:** Genes that are misclassified or whose functions genuinely span multiple categories.
2.  **Outliers:** Experiments with highly unusual gene expression profiles.
3.  **Hard-to-Learn Samples:** Data points that lie in regions where functional categories are thoroughly mixed.

By reducing the 103-dimensional feature space to 2 dimensions using t-SNE and Isomap, we can create powerful visualizations that make these data quality issues apparent.

## Dataset

-   **Source:** [MULAN Repository - Yeast Data]
-   **Instances:** 2,417 (each representing a gene)
-   **Features:** 103 (real-valued gene expression levels)
-   **Labels:** 14 (binary indicators for functional categories, allowing for multi-label assignment)

## Methodology

The project is structured into three main parts as per the assignment guidelines:

### Part A: Preprocessing and Initial Setup
1.  **Data Loading:** The `yeast.arff` file was loaded, and the data was separated into a feature matrix `X` (103 features) and a multi-label target matrix `Y` (14 labels).
2.  **Label Selection for Visualization:** To simplify the visualization, a new categorical target variable was created. This variable isolates the **two most frequent single-label classes** and the **single most frequent multi-label combination**, grouping all other data points into an "Other" category.
3.  **Scaling:** The feature matrix `X` was standardized using `StandardScaler` to ensure all features contribute equally to the distance-based calculations of t-SNE and Isomap.

### Part B: t-SNE and Veracity Inspection
1.  **Hyperparameter Tuning:** t-SNE was run with multiple `perplexity` values (5, 15, 30, 50) to find the optimal setting for visualizing the data structure. A perplexity of **30** was chosen for providing the best balance between local and global structure.
2.  **Visualization:** A 2D scatter plot was generated from the t-SNE output, with points colored according to the categorical variable created in Part A.
3.  **Veracity Analysis:** The resulting plot was carefully inspected to visually identify outliers, noisy labels, and regions of high class overlap.

### Part C: Isomap and Manifold Learning
1.  **Global Structure Visualization:** Isomap was applied to the scaled data to generate a 2D embedding that preserves global, geodesic distances.
2.  **Comparative Analysis:** The Isomap visualization was compared to the t-SNE plot to highlight their fundamental differences (global vs. local structure preservation).
3.  **Manifold Discussion:** The concept of the data manifold was discussed in relation to the Isomap plot, analyzing its complexity and explaining how this complexity directly impacts the difficulty of training an accurate classifier.

## Key Findings & Visualizations

### t-SNE Veracity Inspection

The t-SNE plot (with perplexity=30) successfully revealed distinct clusters and highlighted several data veracity challenges:
-   **Noisy Labels:** Points of one color were found deep within clusters of another, suggesting either misclassification or true biological ambiguity.
-   **Outliers:** Several isolated points were identified, hypothesized to be experimental artifacts or genes with rare, highly specialized functions.
-   **Hard-to-Learn Samples:** A large, dense central region showed a thorough mixing of different categories, illustrating why a simple linear classifier would fail and confirming the need for a non-linear model.


### Isomap and the Data Manifold

The Isomap plot revealed a single, continuous, and curved structure, in contrast to t-SNE's separated clusters.
-   **Global vs. Local Structure:** Isomap proved superior at revealing the global structure, showing that all gene categories belong to a single continuum. t-SNE was better for isolating local clusters.
-   **Complex Manifold:** The plot strongly suggests the data lies on a highly complex and curved manifold. The intermingling of classes along this manifold visually confirms that the classification task is inherently difficult and requires a model capable of learning non-linear decision boundaries.



## Setup and Usage

To reproduce this analysis, clone the repository and set up the environment as described below.

### Prerequisites

You will need Python 3.9+ and the following libraries. You can install them using pip:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```
*Note: `scipy` is a dependency of scikit-learn and will be installed with it.*

### Running the Notebook

1.  Ensure you have the `yeast.arff` dataset file in the specified directory.
2.  Launch Jupyter Notebook or Jupyter Lab:
    ```bash
    jupyter notebook
    ```
3.  Open the `DA5401_A5_Solution.ipynb` file and run the cells sequentially.

## File Structure

```
.
├── DA5401_A5_Solution.ipynb    # The main Jupyter Notebook with code and analysis.
├── data/
│   └── yeast.arff              # The dataset file.
└── README.md                   # This file.
```
