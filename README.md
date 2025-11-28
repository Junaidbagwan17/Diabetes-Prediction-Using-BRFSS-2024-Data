# Step 1 — Importing BRFSS 2024 Data (XPT to CSV Conversion)


Notebook: `Step1_xpt_to_csv_conversion_BRFSS`


In this step, the raw BRFSS 2024 dataset was imported from the CDC website.
Since the data is provided in SAS XPT format, it was converted into a usable CSV format using Python.
This step ensures that the dataset can be easily explored, cleaned, and processed in the following steps.
Data :Available from CDC website:
https://www.cdc.gov/brfss/annual_data/2024/files/LLCP2024XPT.zip

> Tasks performed:

+ Loaded the BRFSS 2024 .XPT file

+ Explored metadata and structure

+ Converted the dataset into .csv

- [x] Saved the CSV file for further analysis.
---
# Step 2 — Data Cleaning and FeatureSelection

Notebook: `Step_2_Data_Cleaning_and_Feature_selection`

In this step, the BRFSS 2024 dataset (converted to CSV in Step 1) was cleaned, validated, and reduced to relevant variables.
The goal of this step is to prepare a high-quality, analysis-ready dataset by handling missing values, removing invalid codes, and selecting key feature.

This stage ensures the dataset is consistent, complete, and suitable for exploratory analysis and machine learning.

> Tasks Performed:

+ Selected key variables from the full BRFSS dataset

+ Created a working copy to preserve original selections

+ Checked missing values across all selected columns

+ Identified invalid codes such as 7, 8, 9, 77, 88, 99

+ Replaced invalid codes with NaN for consistent handling

##### Imputed missing values using:

+ Mode (categorical)

+ Median/mean (numeric, depending on distribution)

+ Removed duplicated columns

+ Verified that no missing data remained after imputation

*Dataset cleaned, imputed, and ready for feature encoding & target mapping in the next step.*
- [x] Saved cleaned dataset as CLEANED_IMPUTED_BRFSS24.csv
