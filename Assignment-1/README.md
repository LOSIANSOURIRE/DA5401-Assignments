# Movie Data Analysis Project  
**Student Name:** Manish Nayak  
**Roll Number:** CE22B069  

***

## Project Overview

This project explores the factors influencing movie success using advanced visualization and statistical analysis. The central hypothesis tested is:  
**“Higher the number of genres, higher is the profit.”**  
By analyzing the relationships between genre count and key movie metrics, the notebook presents a complete data story: from hypothesis formulation and data cleaning, to sophisticated visualizations and concise conclusions.

***

## Folder Structure & Essential Files

```
/
├── tmdb-movies-assignment-1.ipynb    # Main Jupyter notebook with all analysis, plots, and explanations
├── README.md                         # Submission guide and documentation (this file)
```

**Required for evaluation:**  
- `tmdb-movies-assignment-1.ipynb`  
- `README.md`  

***

## How to Evaluate

1. **Open the Notebook:**  
   Start with `tmdb-movies-assignment-1.ipynb` in your Jupyter environment.

2. **Run Sequentially:**  
   Execute all cells in order—the notebook is fully reproducible and self-contained.

3. **Read Markdown Sections:**  
   Explanatory markdown cells precede each major analysis step, describing methodology, reasoning, and interpretation of plots.

***

## Hypothesis and Analytics Walkthrough

### 1. **Hypothesis & Data Preparation**
- The notebook begins with a clear statement of the hypothesis.
- Detailed documentation covers all preprocessing:
    - Handling missing values, outlier removal.
    - Extraction and transformation of genre, crew, and cast columns.
    - Creation of new variables such as profit and number of genres.

### 2. **Key Visualizations**
- **Correlation Heatmap:**  
  Reveals relationships between financial metrics and genre count, axes clearly labeled with units.

- **Barplots:**  
  Show average popularity, revenue, budget, and profit versus number of genres; financial metrics use millions USD, each plot has narrative text blocks.

- **Variance Plots:**  
  Illustrate financial risk (volatility) for different genre counts, units given.

- **Genre Distribution Plot:**  
  Visualizes frequency of movies by number of genres, helping contextualize observed trends.

- **Director-Based Violin Plot:**  
  Compares vote average distributions for the top 5 directors, as per assignment requirements.

### 3. **Assignment-Specific Plots**
- **Pairplot for Success Metrics:**  
  High-level overview of interrelations between budget, revenue, runtime, and ratings.
- **Stacked Area Chart:**  
  Shows movie release trends for top genres over time.
- **Bar Chart (Genre Revenue & Budget):**  
  Compares top genres directly, both revenue and budget on the same axes.
- **Correlation Matrix (Heatmap):**  
  Comprehensive review of all numeric relations.
- **Next Three Bar Plots:**
  Plots specific to the hypothesis

### 4. **Narrative & Conclusion**
- The notebook integrates explanations for each visualization, directly linking them to the hypothesis.
- The conclusion block at the end addresses whether the hypothesis was supported or refuted by the analysis, summarizing all findings.

***

## Where to Find Hypothesis Analysis

- **Hypothesis formulation and supporting plots (barplots, heatmaps, variance plots) are found in the middle sections of the notebook.**
- Each contains a story block and description connecting the plot directly to the hypothesis.
- Final verdict is in the conclusion section.

***

## Notable Code Features

- All monetary values/variances plotted in millions USD for clarity.
- Consistent color palettes for accessibility.
- Comprehensive comments and markdown explain code logic and plot interpretation.

***

## Contact for Clarification

For any questions on methodology, notebook flow, or technical issues, contact:  
**Manish Nayak** (Roll No. CE22B069)

***

**This README gives you the complete roadmap for evaluation and understanding, ensuring transparency and clarity at each step.**
