# Data

This folder contains the dataset used in the NLSY79 income prediction project.

## File

### `IQ.Full.csv`

This dataset is derived from the **National Longitudinal Survey of Youth 1979 (NLSY79)** and contains demographic, family-background, education, cognitive-assessment, and income information for individuals followed over time.

The analysis uses ASVAB test scores collected in 1981 and annual wage and salary income measured in 2005, along with demographic and educational variables. 

---

## Variables Used

The dataset includes:

### Demographic and Education Variables
- `Race` — respondent race category
- `Gender` — respondent gender
- `Educ` — years of education completed
- `MotherEd` — mother's years of education
- `FatherEd` — father's years of education
- `FamilyIncome78` — family income measured earlier in the survey
- `Imagazine` — whether anyone in the household regularly read magazines
- `Inewspaper` — whether anyone in the household regularly read newspapers
- `Ilibrary` — whether anyone in the household had a library card

### Cognitive Ability Measures

The dataset contains ten ASVAB-related subtest scores:

- `Science`
- `Arith`
- `Word`
- `Parag`
- `Numer`
- `Coding`
- `Auto`
- `Math`
- `Mechanic`
- `Elec`

These measures were standardized and used in a Principal Component Analysis to create two summary measures of cognitive ability. 

### Outcome Variable
- `Income2005` — total annual wage and salary income in 2005

Because income was strongly right-skewed, the analysis applies a natural log transformation before modeling. 

---

## Data Preparation

The notebook performs the following preprocessing steps:

1. Removes the respondent ID variable from the modeling dataset.
2. Recodes gender as a binary variable.
3. Applies a natural log transformation to `Income2005`.
4. Separates the final observation for an individual holdout prediction.
5. Divides the remaining observations into:
   - **70% training**
   - **20% testing**
   - **10% validation**
6. Standardizes the ten ASVAB variables before PCA. 

---

## Notes

The dataset is observational, so relationships identified in the analysis should be interpreted as **associations rather than causal effects**.

Important determinants of income such as occupation, industry, labor-market conditions, and other personal circumstances are not included in the available dataset. 
