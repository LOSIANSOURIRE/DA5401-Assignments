# DA5401 A8: Ensemble Learning for Complex Regression Modeling
**NAME:** Manish Nayak  
**ROLL NO:** CE22B069


This project explores the application of advanced ensemble learning techniques—Bagging, Boosting, and Stacking—to solve a complex, time-series regression problem. The goal is to accurately forecast the hourly demand for a city's bike-sharing program using the [Bike Sharing Demand Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset) from the UCI Machine Learning Repository.

The project demonstrates a systematic approach to model improvement, starting from a simple baseline and progressively building more sophisticated models to minimize prediction error, measured by Root Mean Squared Error (RMSE).

## Project Objective

To apply, compare, and evaluate three primary ensemble techniques (Bagging, Boosting, and Stacking) to accurately predict the total count of rented bikes (`cnt`). The project showcases how these methods address model variance and bias, and how a diverse stack of models can yield superior performance to any single model.

## Dataset

*   **Name:** Bike Sharing Demand Dataset (Hourly Data)
*   **Source:** UCI Machine Learning Repository
*   **Instances:** ~17,000 hourly samples with 16 features.
*   **Target Variable:** `cnt` (total count of bike rentals).

The dataset contains rich information about weather, time of day, season, and holidays, making it ideal for a complex regression task with non-linear relationships.

## Project Structure

The project is structured in a single Jupyter Notebook (`assignment-8-notebook.ipynb`) and is divided into four main parts:

**Part A: Data Preprocessing and Baseline**
1.  **Data Loading:** Fetches the dataset directly from the UCI repository using the `ucimlrepo` library.
2.  **Feature Engineering:** Cleans the data by dropping irrelevant columns and performs one-hot encoding on categorical features (`season`, `weathersit`, `hr`, etc.) to prepare them for regression models.
3.  **Train/Test Split:** Splits the data into an 80% training set and a 20% testing set.
4.  **Baseline Models:** Trains a `DecisionTreeRegressor` and a `LinearRegression` model. The model with the lower RMSE is selected as the performance baseline.

**Part B: Ensemble Techniques for Bias and Variance Reduction**
1.  **Bagging:** Implements a `BaggingRegressor` using the Decision Tree as the base estimator to demonstrate variance reduction.
2.  **Boosting:** Implements a `GradientBoostingRegressor` to demonstrate bias reduction by sequentially correcting errors.

**Part C: Stacking for Optimal Performance**
1.  **Stacking Implementation:** Builds a `StackingRegressor` that combines three diverse base learners (`KNeighborsRegressor`, the `BaggingRegressor`, and the `GradientBoostingRegressor`).
2.  **Meta-Learner:** Uses a `Ridge` regression model as the final meta-learner to optimally combine the predictions of the base models.

**Part D: Final Analysis**
1.  **Comparative Table:** Summarizes the RMSE scores of all five models for a clear performance comparison.
2.  **Conclusion:** Provides an in-depth analysis of why the best-performing model was successful, referencing the bias-variance trade-off and the principle of model diversity.

## Key Findings and Results

The project successfully demonstrated a clear hierarchy of model performance, with each successive ensemble technique providing a significant improvement.

| Model                       | RMSE       | Performance Improvement |
| :-------------------------- | :--------- | :---------------------- |
| **Linear Regression (Baseline)** | 100.4449   | **Baseline**            |
| Bagging Regressor           | 112.2620   | -11.77%                 |
| Gradient Boosting Regressor | 54.1999    | +46.04%                 |
| **Stacking Regressor**      | **49.4370**    | **+50.78%**             |

*   **Gradient Boosting** provided the most significant leap in performance, nearly halving the baseline error. This indicated that the primary challenge of the dataset was high **bias**, which the boosting algorithm effectively minimized.
*   The **Stacking Regressor** achieved the best overall result, proving that intelligently combining the predictions of diverse models can lead to a final model that is more accurate and robust than any of its individual components.

## How to Run This Project

### Prerequisites
*   Python 3.x
*   Jupyter Notebook or JupyterLab
*   Required Python libraries:
    *   `pandas`
    *   `numpy`
    *   `scikit-learn`
    *   `ucimlrepo`

### Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```
2.  **Install the required packages:**
    The `ucimlrepo` library will be installed by the first cell in the notebook, but you can also install all dependencies via pip:
    ```bash
    pip install pandas numpy scikit-learn ucimlrepo jupyterlab
    ```

### Execution

1.  **Launch Jupyter:**
    ```bash
    jupyter lab
    ```
2.  **Open and Run the Notebook:**
    Open the `assignment-8-notebook.ipynb` file and run the cells sequentially from top to bottom. The notebook is self-contained and will automatically fetch the dataset and run all experiments. The final markdown cells contain the complete analysis and conclusion.
