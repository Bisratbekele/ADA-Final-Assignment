# Association Between Vitamin D Levels and Depression: NHANES 2021-2023 Analysis

## Project Description

This repository includes the NHANES 2021-2023 dataset and R Markdown code used to analyze the association between serum Vitamin D levels and depression among U.S. adults. The project examines whether Vitamin D deficiency is associated with increased odds of depression after adjusting for demographic and health-related confounders.

## Files Included

- `DEMO_L.xpt`: Demographics dataset from NHANES 2021-2023
- `VID_L.xpt`: Vitamin D laboratory measurements
- `DPQ_L.xpt`: Depression screening (PHQ-9) questionnaire data
- `BMX_L.xpt`: Body measurements (BMI)
- `SMQ_L.xpt`: Smoking questionnaire data
- `VitD_Depression_Analysis.Rmd`: R Markdown script for the complete analysis
- `README.md`: This file

## What the Code Does

### Data Preparation
- Imports five NHANES datasets from GitHub repository
- Merges datasets by participant ID (SEQN)
- Calculates PHQ-9 total scores and creates binary depression outcome (PHQ-9 ≥ 10)
- Creates categorical Vitamin D variable (Deficient <50, Insufficient 50-74, Sufficient ≥75 nmol/L)
- Recodes demographic variables (age, sex, race/ethnicity, education)
- Creates categorical BMI variable (Normal/Underweight, Overweight, Obese)
- Creates smoking status variable

### Data Exploration
- Examines missing data patterns for all variables
- Generates descriptive statistics
- Creates boxplot visualization of Vitamin D levels by depression status
- Performs complete case analysis

### Statistical Analysis
- Tests linearity assumptions using Box-Tidwell technique for continuous predictors
  - **Result**: Non-linearity detected for Vitamin D and BMI → used categorical versions
  - **Result**: Linearity assumption met for age → kept as continuous
- Runs univariate logistic regression (Vitamin D categories → Depression)
- Runs multivariate logistic regression adjusting for:
  - Age (continuous)
  - Sex
  - Race/Ethnicity
  - BMI categories
  - Education
  - Income-to-poverty ratio
  - Smoking status

### Model Diagnostics
- Checks for multicollinearity using VIF
- Identifies influential observations using Cook's Distance
- Evaluates model performance with ROC curve and AUC

### Output
- Generates Table 1: Descriptive statistics by depression status
- Exports results as HTML and Word document

## How to Run the Code

1. **Download or clone this repository** to your computer
   ```bash
   git clone https://github.com/Bisratbekele/ADA-Final-Assignment.git
   ```

2. **Install required R packages** (if not already installed)
   ```r
   install.packages("pacman")
   pacman::p_load(ggplot2, car, odds.n.ends, dplyr, tidyr, haven, table1)
   ```

3. **Open `VitD_Depression_Analysis.Rmd`** in RStudio

4. **Set your working directory** to the folder where the files are saved
   
5. Run code chunks sequentially
   
## Key Variables

### Exposure Variable
- **Vitamin D Categories** (vitd_category):
  - Deficient: <50 nmol/L
  - Insufficient: 50-74 nmol/L
  - Sufficient: ≥75 nmol/L (Reference group)

### Outcome Variable
- **Depression** (depression_binary):
  - PHQ-9 ≥ 10: Depression (moderate to severe symptoms)
  - PHQ-9 < 10: No Depression (Reference group)

### Covariates
- Age (continuous, years)
- Sex (Male/Female)
- Race/Ethnicity (6 categories)
- BMI categories (Normal/Underweight, Overweight, Obese)
- Education (5 levels)
- Income-to-poverty ratio (continuous)
- Smoking status (Ever/Never smoker)

## Key Findings

### Univariate Analysis
Compared with participants with **sufficient** vitamin D:
- Those with **insufficient** vitamin D have **46% higher odds** of depression (OR = 1.46, 95% CI: 1.18–1.80, p < 0.001)
- Those with **deficient** vitamin D have **81% higher odds** of depression (OR = 1.81, 95% CI: 1.44–2.27, p < 0.001)

### Multivariate Analysis
The strong unadjusted associations were largely explained by confounding variables (especially age, sex, income-to-poverty ratio, and smoking). 
After adjustment, the associations weakened considerably and lost statistical significance.
## Data Source

All data are from the **National Health and Nutrition Examination Survey (NHANES) 2021-2023**:
- CDC NHANES Website: https://www.cdc.gov/nchs/nhanes/
- GitHub Repository: https://github.com/Bisratbekele/ADA-Final-Assignment

## Study Limitations

1. **Cross-sectional design**: Cannot establish causality or temporal sequence
2. **Missing data**: Complete case analysis may introduce selection bias
3. **Unmeasured confounding**: Possible residual confounding from unmeasured variables
4. **Self-reported outcomes**: Depression assessed via PHQ-9 questionnaire (not clinical diagnosis)

## Study Strengths

1. **Nationally representative sample**: NHANES uses complex survey design
2. **Standardized measures**: Laboratory-measured Vitamin D and validated PHQ-9 instrument
3. **Comprehensive adjustment**: Adjusted for multiple demographic and health confounders
4. **Transparent analysis**: Fully documented and reproducible R Markdown workflow
5. **Appropriate statistical methods**: Box-Tidwell tests informed variable specification

## Software and Packages

**R Version**: 4.4 

**Required Packages**:
- `ggplot2`: Data visualization
- `car`: VIF and diagnostics
- `odds.n.ends`: Odds ratios and model evaluation
- `dplyr`: Data manipulation
- `tidyr`: Data tidying
- `haven`: Import XPT files
- `table1`: Descriptive tables

## References

1. Anglin RE, Samaan Z, Walter SD, McDonald SD. Vitamin D deficiency and depression in adults: systematic review and meta-analysis. *Br J Psychiatry*. 2013;202:100-7.

2. Musazadeh V, et al. Vitamin D protects against depression: Evidence from an umbrella meta-analysis on interventional and observational meta-analyses. *Pharmacol Res*. 2023;187:106605.

3. Centers for Disease Control and Prevention. NHANES 2021-2023 Data Documentation. Available: https://www.cdc.gov/nchs/nhanes/

4. Kroenke K, Spitzer RL, Williams JB. The PHQ-9: validity of a brief depression severity measure. *J Gen Intern Med*. 2001;16(9):606-13.

## Author

- **Name**: Bisrat Bekele
- **Program**: MPH - Epidemiology & Biostatistics
- **Institution**: Washington University in St. Louis
- **Course**: Fall_2025.PHCC.6009.01 - Advanced Data Analysis
- **Date**: November 2025

