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
---
# Step 4 — EDA and Hypothesis Testing

Notebook: `Step4_EDA_and_HypothesisTesting.ipynb`

In this step, the cleaned BRFSS 2024 dataset was explored using Univariate and Bivariate EDA to understand the overall structure, distributions, and relationships among the variables.
Additionally, statistical hypothesis tests (Chi-square tests) were performed to validate the observed relationships with diabetes status.

The goal of this step is to uncover meaningful patterns, detect skewness/outliers, and statistically confirm which features show significant differences between diabetic and non-diabetic individuals.

>  Tasks Performed
>> Univariate Analysis

+ Visualized the distribution of key variables such as Age, BMI, Physical Health Days, Life Satisfaction, Income, and Education.

+ Identified skewness, outliers, and imbalanced categories.

+ Summarized patterns relevant for later feature engineering and modeling.

>> Bivariate Analysis

Explored how major predictors relate to diabetes status using bar plots and proportion charts.
Compared categories such as:

+ General Health vs Diabetes

+ Income Level vs Diabetes

+ Exercise Status vs Diabetes

+ Life Satisfaction vs Diabetes

>> Hypothesis Testing (Chi-Square Tests)

Performed Chi-square tests to validate associations between categorical predictors and diabetes.

Significant relationships were found for:

+ General Health vs Diabetes

+ Income Group vs Diabetes

+ Exercise Status vs Diabetes

+ Education Level vs Diabetes

*Results confirmed that several health and demographic factors differ meaningfully between diabetic and non-diabetic individuals.*

>> Hyoothesis Outcomes Cheking using BRFSS Data

This step produced:

Clear distribution plots for understanding data behavior.
Relationship insights showing which features are strongly linked to diabetes.
Statistically validated evidence supporting the patterns seen in visualizations.
A solid analytical foundation that guides feature selection and model building in the next step.

- [x] The dataset is now well-understood, and the key predictors influencing diabetes have been statistically confirmed — ready for Step 5: Data Preprocessing for Modeling.

----
# Step 5 — Data Preprocessing for Modeling

Notebook: `Step5_Data_Preprocessing_for_Model.ipynb`

In this step, the cleaned BRFSS dataset was transformed into a fully model-ready format.
Numeric and categorical features were standardized, encoded, and optimized to ensure that machine learning algorithms receive consistent, meaningful inputs.

The goal of this step was to prepare high-quality, standardized features while preventing data leakage and preserving model integrity.

> Tasks Performed:

+ Identified and selected all numeric columns
+ Used select_dtypes() to gather int64 and float64 variables.
+ Removed the target variable DIABETE4 from this list to avoid leakage.
+ Converted BMI to real BMI values
+ Transformed _BMI5 by dividing by 100 to convert BRFSS’s stored BMI (×100) into actual BMI.
+ Mapped age category _AGEG5YR into meaningful numeric midpoints
+ Replaced ordinal category codes with midpoint age values for more realistic modeling.
+ Applied One-Hot Encoding for race
+ Created binary indicator variables using pd.get_dummies() for _IMPRACE.
+ Checked for missing values & verified distributions
+ Ensured clean, valid numeric ranges before scaling.
- Standardized all numeric features using StandardScaler
- Scaled features to mean = 0 and standard deviation = 1 to improve model stability and training performance.
- (Note: Scaling should be done after train-test split to avoid leakage. souece - GOOGLE) 
Ensured that label-mapped columns were excluded from modeling
Only numeric, model-safe columns were retained for training and evaluation.

> Outcome
The dataset is now fully preprocessed, containing:
- Well-scaled numeric features

- Properly encoded categorical variables

- Corrected age and BMI representations

- Clean, consistent inputs ready for machine learning algorithms

- [x] Generated a complete model-ready dataset for Step 6 — Model Building & Training

