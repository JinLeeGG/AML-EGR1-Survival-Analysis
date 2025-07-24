# Survival Prediction Model for AML using Gene Expression Data from TCGA

## 1\. Overview

This project analyzes the relationship between the expression levels of specific genes and patient survival outcomes in Acute Myeloid Leukemia (AML). The analysis utilizes data from The Cancer Genome Atlas (TCGA-LAML) cohort.

The primary goal is to identify significant prognostic biomarkers through survival analysis and to build a machine learning model that predicts patient survival status based on gene expression data.

## 2\. Key Features

  - **Data Preprocessing:** Cleans and merges RNA-seq expression data and clinical data downloaded from cBioPortal, aligning them by patient ID.
  - **Survival Analysis:**
      - Stratifies patients into groups (e.g., High vs. Low expression) based on the expression levels of specific genes (`EGR1`, `MAFB`, etc.).
      - Visualizes survival differences between groups using Kaplan-Meier curves.
      - Validates the statistical significance of these differences using the log-rank test.
  - **Machine Learning Modeling:**
      - Develops and trains Logistic Regression and Random Forest models to predict patient survival status (Deceased/Living).
      - Evaluates model performance using metrics such as Accuracy, Precision, and Recall.
      - Identifies the most influential genes for survival prediction using the Random Forest's feature importance scores.

## 3\. Data Source

  - **Platform:** [cBioPortal for Cancer Genomics](https://www.cbioportal.org/)
  - **Study Dataset:** `Acute Myeloid Leukemia (TCGA, PanCancer Atlas)`
  - **Required Files:**
    1.  `Clinical Data`
    2.  `mRNA Expression (RNA-seq RSEM)`

## 4\. Installation

### A. Prerequisites

  - Python 3.8 or higher

### B. Installing Dependencies

You can install all required libraries at once using the following command:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn lifelines
```

Alternatively, create a `requirements.txt` file in the project directory with the content below.

**requirements.txt**

```
pandas
numpy
matplotlib
seaborn
scikit-learn
lifelines
jupyterlab
```

Then run the following command to install them:

```bash
pip install -r requirements.txt
```

## 5\. Usage

1.  **Download Data**

      - Download the two required files listed in the "Data Source" section.
      - Place them inside a `data/` directory within the project folder. (Create the directory if it doesn't exist).

2.  **Launch Jupyter Notebook**

      - Open your terminal and run the following command to start Jupyter Lab:

    <!-- end list -->

    ```bash
    jupyter lab
    ```

3.  **Run the Analysis**

      - Open the `AML_Survival_Analysis.ipynb` notebook (or your custom notebook file).
      - Execute the cells sequentially to perform the data preprocessing, analysis, and modeling.

## 6\. Key Results

  - **Survival Analysis:** A statistically significant difference in survival was observed between the high and low `EGR1` expression groups (log-rank test p-value \< 0.05). The high-expression group was associated with a better survival prognosis.
  - **Machine Learning Prediction:**
      - **(Example)** The Random Forest model achieved approximately 78% accuracy in predicting survival status, outperforming the Logistic Regression model (approx. 71%).
      - **(Example)** Feature importance analysis revealed that `EGR1` was a more significant predictor of survival than `MAFB` in the model.

## 7\. Technologies Used

  - **Language:** Python
  - **Libraries:**
      - **Data Handling:** Pandas, NumPy
      - **Visualization:** Matplotlib, Seaborn
      - **Survival Analysis:** Lifelines
      - **Machine Learning:** Scikit-learn
  - **IDE:** Jupyter Lab / Jupyter Notebook
