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
---
#  Step 3 — Mapping Categorical Variables to Meaningful Labels

**Notebook:** `Step3_Mapping_variables_For_EDA.ipynb`

In this step, categorical variables in the cleaned BRFSS dataset were converted into **human-readable labels**.  
The original numeric codes (1, 2, 3, 4..) were mapped to descriptive text values such as *“Yes”*, *“No”*, *“Male”*, *“Female”*, *“Excellent”*, *“Poor”*, etc.

This step improves clarity during EDA and makes graphs, summaries, and relationships easier to interpret.


> Tasks Performed:

+ Created label-mapped versions of categorical columns using `_LABEL` suffix  
  Example:
  `SMOKE100' to SMOKE100_LABEL as {1: 'Yes', 2: 'No'}`

+ Mapped categorical codes for all selected features into descriptive text labels

+ Ensured original numeric columns remained untouched for modeling purposes

+ Prepared dataset for cleaner, more readable EDA visualizations

+ Verified label mappings to avoid missing or incorrectly assigned categories

*Dataset now includes readable `_LABEL` columns, improving interpretation and visualization in the upcoming EDA step.*

- [x] Saved including both numerical and ordinal Categorial data as CLEANED_LABELED_BRFSS2024.csv
