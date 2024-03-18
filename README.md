# Capstone-Project
CIND820

# Project: Predicting Employment Status in Canada

# Title: Can Machine Learning Algorithms Accurately Predict Individuals' Employment Status Based on Occupation, Immigration Levels, and Other Demographic Factors?

## Approach
This project addresses the challenge of determining the true demographic factors influencing employment status in Canada, with a specific focus on the role of occupation, and immigration. 

### Stages of the Project

1. **Problem Identification**: Understanding the influence of immigration status and occupations on employment status and identifying other demographic factors leading to unemployment.

2. **Data Acquisition**: Obtaining the Canadian Labour Force Survey from Statistics Canada's official website.

3. **Data Preparation**:
   - Performing descriptive analysis of the dataset.
   - Converting data types from `int64` and `float64` to `category` and `uint8` for ordinal and nominal data, respectively.
   - Applying one-hot encoding to nominal data.
   - Removing columns with missing values.
   - Dealing with missing values through various alternative methods. Each of the three models was developed using the alternatives below separately:
     - **ALTERNATIVE_1 Imputation**: Features `NAICS_21` and `NOC_10` (with 37,045 missing values out of 108,024) using `KNN`, and `Union` (with 52,795 missing values) were imputed by replacing the all missing values with category 0(refers to not a union member).
     - **ALTERNATIVE_2 Removing**: The `Union` column was completely removed, and rows with missing values for `NAICS_21` and `NOC_10` were also removed. Subsequent analysis was then conducted with 70,979 instances.
     - **ALTERNATIVE_3 Imputation and Removing**: For this alternative, `Union` was removed entirely, and the missing values for `NAICS_21` and `NOC_10` were imputed.
       - The missing values for `Union` were not imputed because the absence of these values was attributed to unemployment itself. This was verified by filtering the Employment Status Category 1 (Employed) against the Union categories, revealing that all missing values in `Union` originated from the Unemployed group (Category 0).
   - Applying `SMOTE` to deal with imbalanced data: The class data in the alternative 2 above were imbalanced. The SMOTE technique was applied to address this class imbalance.
4. **Feature Engineering**:
   - Binarizing the `lfsstat` variable to create a balanced binary class attribute. (Originally there were 4 categories: Employed, at work;       Employed, absent from work; Unemployed; and Not in labour force. First two were recatogorized into category 1, and the rest in category      0)
   - Selecting features based on Spearman’s Rank Correlation.

5. **Model Selection and Training**:
   - Choosing Random Forest, Extreme Gradient Boost, and Logistic Regression for their robustness with categorical data.
   - Spliting the data using an 80:20 ratio.
   - Employing 10-fold cross-validation for training and testing.
   - `Hyperparameter Tunining` was performed using `Randomized Search`.

6. **Model Evaluation**:
   - Executing the three algorithms.
   - Comparing F1 scores for the scenario of using ALTERNATIVE_2 above.
   - Using the Friedman test for statistical comparison of the models.
   - Created two alternative codes for the Alternatives that was created during the data preparation. These codes should be run according to the selection of the method of dealing with missing values. However, the Alternative 2 is selected and its following codes throughout the model selection, training, and evaluation were executed.


## References
Cross, P. (2021). The Implications of Slowing Growth in Canada's Labour Force. Fraser Institute.

FAO (2023). Labour Market Outcomes of Immigrants in Ontario and its Major Cities. https://www.fao-on.org/en/Blog/Publications/ilmo 

Montgomery, E. (1989). Employment and unemployment effects of unions. Journal of Labor Economics, 7(2), 170-190.

Nachev, A., & Teodosiev, T. (2018). Analysis of Employment Data Using Support Vector Machines. International Journal of Applied Engineering Research, 13(18), 13525-13535. Retrieved from http://www.ripublication.com

Gorodzeisky, A., & Semyonov, M. (2017). Labor force participation, unemployment and occupational attainment among immigrants in West European countries. PloS one, 12(5), e0176856.

Guo, T., Xia, F., Zhen, S., Bai, X., Zhang, D., Liu, Z., & Tang, J. (2019). Graduate Employment Prediction with Bias. https://doi.org/10.48550/arxiv.1912.12012

Huot, S., Chen, X., King, C., Painter-Zykmund, E., & Watt, K. (2016). Making difficult decisions: Immigrants’ experiences of employment preparation and participation. Work, 54(3), 709-720.

Premalatha, N., & Sujatha, S. (2021). An Effective Ensemble Model to Predict Employment Status of Graduates in Higher Educational Institutions. In 2021 Fourth International Conference on Electrical, Computer and Communication Technologies (ICECCT). IEEE.

Statistics Canada (2024). Labour Force Survey: Public Use Microdata File, December 2023. Retrieved from: https://www150.statcan.gc.ca/n1/en/catalogue/71M0001X


