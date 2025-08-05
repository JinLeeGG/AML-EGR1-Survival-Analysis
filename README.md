# Analysis of EGR1 Gene Expression and Survival in Acute Myeloid Leukemia (AML) Patients, and Building a Predictive Machine Learning Model 

## Project Overview

The goal of this project is to **analyze the statistical association between the expression level of the EGR1 (Early Growth Response 1) gene and the survival outcomes of patients with Acute Myeloid Leukemia (AML)**, using data from the [AML database of the Human Cancer Genome Atlas (TCGA - LAML)](https://gdc.cancer.gov/about-data/publications/laml_2012). Additionally, the project will involve the development of a machine learning model that predicts patient survival status based on RNA expression data.

The project is structured into three main stages:

1.  **Data Preprocessing and Analysis**: Cleaning and integrating clinical and RNA-seq data into a format suitable for analysis.
2.  **Survival Analysis**: Statistically verifying the impact of EGR1, MAFB gene expression levels on patient survival duration using Kaplan-Meier analysis and the log-rank test.
3.  **Machine Learning Modeling**: Building and evaluating a classification model to predict patient survival status (Alive/Deceased) using gene expression data as features.

## Hypothesis

In a cohort of patients with Acute Myeloid Leukemia (AML), differences in EGR1 gene expression levels will be correlated with statistically significant differences in survival outcomes. 

## Dataset

  - **Data Source**: [AML database of the Human Cancer Genome Atlas (TCGA - LAML)](https://gdc.cancer.gov/about-data/publications/laml_2012)
  - **Sample Size**: 200 patients with Acute Myeloid Leukemia (AML)
  - **Data Types**:
      - Patient Clinical Data
      - RNA-seq Gene Expression Data (RNAseq GAF 2.0 read count)


## Project Pipeline

### 1\. Data Analysis and Preprocessing (`1_Data_Analysis_Preprocessing.ipynb`)

  - **Clinical Data Processing**:

      - Extracted key information for analysis: `bcr_patient_barcode` (patient ID), `vital_status`, `days_to_death`, and `days_to_last_followup`.
      - Created a derived feature, `Observation Period`, representing the total observation time by using `days_to_death` for deceased patients and `days_to_last_followup` for living patients.
      - Converted `vital_status` into a binary `Status` variable (Deceased: 1, Alive: 0) for survival analysis.

  - **RNA Expression Data Processing**:

      - Removed 123 genes with missing information ('?') from the initial 20,442 genes.
      - Cleaned the `GeneID` format to `{gene_name}|{id}` for ease of analysis.
      - Transposed the data matrix so that each row represents a patient and each column represents a gene's expression level.

  - **Data Integration**:

      - Merged the cleaned clinical and RNA expression data on the patient ID (`bcr_patient_barcode`) to create the final analytical dataset (`merged_df.csv`).

### 2\. Survival Analysis (`2_Survival_Analysis_of_EGR1_Expression_in_Patients_with_Acute_Myeloid_Leukemia.ipynb`)

  - **Kaplan-Meier Survival Analysis**:

      - Stratified patients into two groups based on the expression levels of `EGR1` and `MAFB` genes: the top 20% (High Expression) and the bottom 20% (Low Expression).
      - Visualized and compared the survival probabilities over time between the two groups.

  - **Log-rank Test**:

      - Statistically tested whether the difference between the survival curves of the two groups was significant, using the p-value.

### 3\. Machine Learning Modeling (`3_Machine_Learning_Modeling.ipynb`)

  - **Feature and Target Definition**:

      - **Features (X)**: 20,319 gene expression data points.
      - **Target (y)**: `Status` (patient's survival status).

  - **Model Training and Evaluation**:

      - **Attempt 1**: Evaluated the performance of Logistic Regression and Random Forest models using all gene expression data as features.
      - **Attempt 2 (Feature Selection)**: Used the results from the log-rank test to select 2,825 significant genes (p-value ≤ 0.05) as features. Re-evaluated the models to determine if performance improved.


## Key Findings

### Survival Analysis Results

  - **EGR1**: The high-expression group (top 20%) showed a **significantly higher survival probability** compared to the low-expression group (bottom 20%) (p-value = 0.01).

    <img width="584" height="455" alt="EGR1" src="https://github.com/user-attachments/assets/4c778ef1-ed9e-4b03-ab58-a062788d21b3" />

    
  - **MAFB**: The low-expression group (low 20%) showed a **significantly higher survival probability** compared to the high-expression group (high 20%) (p-value = 0.01).

    <img width="567" height="455" alt="MAFB" src="https://github.com/user-attachments/assets/5ec2a134-9362-4d19-9fb4-08ef04da9599" />


### Machine Learning Model Performance

  - The **Random Forest model achieved the highest predictive accuracy at 67.6%** when trained on the set of significant genes.
  - The performance of the Random Forest model slightly improved after feature selection, suggesting that dimensionality reduction can contribute to better model performance.

    | Model | Feature Set | Accuracy |
    | :--- | :--- | :--- |
    | Logistic Regression | All Genes (20,319) | 56.0% |
    | Random Forest | All Genes (20,319) | 65.0% |
    | Logistic Regression | Significant Genes (2,825) | 47.0% |
    | **Random Forest** | **Significant Genes (2,825)** | **67.6%** |

