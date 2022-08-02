# Holmusk Challenge

## Finding Factors Driving Cost Of Care

Ray Tan

### Task

The task is to analyse the clinical and financial data of patients hospitalised for a certain condition. Some variable names and patient id's have been anonymised in this dataset. It is required to join the data given in different tables, and find insights about the drivers of cost of care.

### Background

Healthcare costs in Singapore have been rising and are expected to keep increasing over the coming years [[1]](https://www.dbs.com.sg/personal/articles/nav/protection/guide-health-insurance-singapore-medishield-medisave?pid=sg-dbs-pweb-insure-product-firstinsurance-image-textlink-medishield-medisave). Part of the rising costs have been attributed to health insurance policies with full riders that cover hospital bills in full as they may have contributed to over-consumption by policyholders and over-charging of medical services [[2]](https://www.dbs.com.sg/personal/articles/nav/protection/integrated-shield-plans). Health insurers have had to adjust the terms for full-rider health insurance policies to require co-payment of hospital bills in order to keep healthcare costs down [[3]](https://www.straitstimes.com/singapore/health/moh-welcomes-measures-by-insurers-to-adjust-terms-for-full-rider-ips-and-require-co).

### Problem Statement

Against a backdrop of rising healthcare costs, ABC Health Insurance would like to understand the factors driving cost of care in order to structure their policy offerings in a way that remains competitive, attractive, and sustainable in the long run. To achieve this, they need to ensure that premiums are kept affordable, that plans are able to meet the needs of policyholders, and that claim payouts do not exceed cash revenue.

### Objectives

The objectives of this project are to:
- Explore the data and visualise individual variables as well as the relationships between independent variables and bill amount
- Predict bill amount by training 3 regression models (linear, ridge, lasso) and evaluate them using 2 metrics (R², RMSE) to select the best performing model
- Analyse the final model for the accuracy of its predictions and the weights of its features
- Find the main factors driving cost of care (i.e. the features which are most important in explaining bill amount)
- Make recommendations that address the issue of rising healthcare costs

### Data Sources

The following datasets were used:

* [`bill_amount.csv`](../data/bill_amount.csv): Bill Amount Dataset

> This dataset contains a listing of the bill IDs and the corresponding bill amounts. There are 13,600 rows and 2 columns.

* [`bill_id.csv`](../data/bill_id.csv): Bill ID Dataset

> This dataset contains a listing of the bill IDs and the corresponding patient IDs and dates of admission. It is from the period 2011 to 2015. There are 13,600 rows and 3 columns.

* [`clinical_data.csv`](../data/clinical_data.csv): Clinical Dataset

> This dataset contains a listing of the patient IDs and the dates of admission. It is from the period 2011 to 2015. For each patient admission, there is information on the patient's date of discharge, medical histories, pre-op medications, symptoms, lab results, weight, and height. There are 3,400 rows and 26 columns.

* [`demographics.csv`](../data/demographics.csv): Demographics Dataset

> This dataset contains a listing of the patient IDs and their corresponding gender, race, resident status, and date of birth. There are 3,000 rows and 5 columns.

### Data Dictionary

A description of the variables found across all the datasets is given below:

| Variable | Type | Description |
|:---|:---|:---|
| patient_id | object | Patient identification |
| date_of_admission | datetime | Date of admission (in YYYY-MM-DD) |
| date_of_discharge | datetime | Date of discharge (in YYYY-MM-DD) |
| date_of_birth | datetime | Date of birth (in YYYY-MM-DD) |
| gender | object | Gender |
| race | object | Race |
| resident_status | object | Resident status |
| year_of_admission | object | Year of admission |
| month_of_admission | object | Month of admission |
| medical_history_1 | integer | Presence of medical history 1 |
| medical_history_2 | integer | Presence of medical history 2 |
| medical_history_3 | integer | Presence of medical history 3 |
| medical_history_4 | integer | Presence of medical history 4 |
| medical_history_5 | integer | Presence of medical history 5 |
| medical_history_6 | integer | Presence of medical history 6 |
| medical_history_7 | integer | Presence of medical history 7 |
| preop_medication_1 | integer | Presence of pre-op medication 1 |
| preop_medication_2 | integer | Presence of pre-op medication 2 |
| preop_medication_3 | integer | Presence of pre-op medication 3 |
| preop_medication_4 | integer | Presence of pre-op medication 4 |
| preop_medication_5 | integer | Presence of pre-op medication 5 |
| preop_medication_6 | integer | Presence of pre-op medication 6 |
| symptom_1 | integer | Presence of symptom 1 |
| symptom_2 | integer | Presence of symptom 2 |
| symptom_3 | integer | Presence of symptom 3 |
| symptom_4 | integer | Presence of symptom 4 |
| symptom_5 | integer | Presence of symptom 5 |
| lab_result_1 | float | Reading of lab result 1 |
| lab_result_2 | float | Reading of lab result 2 |
| lab_result_3 | float | Reading of lab result 3 |
| weight | float | Weight (in kg) |
| height | float | Height (in cm) |
| bmi | float | Body mass index (in kg/m²) |
| age_at_admission | integer | Age at admission |
| days_hosp | integer | Days hospitalised |
| hosp_count | integer | Hospitalisation count |
| days_since_last_hosp | integer | Days since last hospitalisation |
| num_of_medical_histories | integer | Number of medical histories |
| num_of_preop_medications | integer | Number of pre-op medications |
| num_of_symptoms | integer | Number of symptoms |
| bill_amount | float | Bill amount (in $) |

### Data Warehouse

A list of the datasets that have been exported is given below:

* [`health_cleaned.csv`](../data/health_cleaned.csv): Health Dataset Cleaned
* [`health_engineered.csv`](../data/health_engineered.csv): Health Dataset Engineered
* [`health_selected.csv`](../data/health_selected.csv): Health Dataset Selected

### Recommendations

Some recommendations can be made based on the analysis of the data.

#### 1. Symptoms & Medical Histories

`symptom_5`, `medical_history_1`, and `medical_history_6` are key features that have a significant influence on the bill amount. ABC Health Insurance could construct all their policies to include mandatory entry-level coverage of these conditions so that there will be a large base of paying customers to shoulder the costs of claim payouts, which are expected to be huge. This has the dual advantage of keeping the premiums affordable and ensuring that patients who have these conditions receive adequate monetary benefits.

#### 2. Race

`race` is a factor that plays a huge role in deciding the bill amount. Malay patients are predicted to have the highest bill amount, followed by Indian patients, Other patients, and then Chinese patients. ABC Health Insurance would need to conduct further studies to investigate if there are confounding variables that could explain the racial differences in the bill amount and incorporate those findings in their policies. [Ethnic predisposition to different diseases](https://psomagen.com/race-and-predisposition-to-disease/) is a frequently-discussed topic. In Singapore, this [newspaper article](https://www.straitstimes.com/singapore/health/malay-population-the-most-unhealthy-group-in-singapore) highlighted that a disproportionate number of patients with diabetes, kidney failure, heart attack, and stroke come from the Malay population. Hence, Malay patients could be incurring higher bill amounts than their racial counterparts because they might be more inclined to chronic diseases which would increase their hospitalisation burden.

#### 3. Weight

`weight` is a factor that has a moderately important place in determining the bill amount. Patients with heavier weights are predicted to have larger bill amounts. A [systematic literature review on the economic burden for obesity](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5409636/) discovered that obesity is responsible for a large fraction of costs for both healthcare systems and the society. However, insurance companies are still divided on [whether to view obesity as a disease or not](https://www.healthline.com/health/is-obesity-a-disease). ABC Health Insurance could start to make provisions recognising obesity as a disease and begin to provide coverage and benefits for patients seeking obesity treatment.

### Limitations

There are a few limitations to this project.

#### 1. Absence of critical features

Information on some of the major determinants of hospitalisation costs such as type of surgery, experience of attending doctor, any imaging done, ward class, admission to an intensive care unit or a high dependency unit, and treatment at a public hospital or private hospital are absent. This [study on the predictors of acute hospital costs](https://www.ahajournals.org/doi/full/10.1161/01.STR.30.4.724) found that room charges account for 50% of hospitalisation costs. The presence of these predictors could potentially lead to a better estimation of bill amount and provide a stronger understanding of the factors driving the cost of care.

#### 2. Inadequacy of existing features

Due to an anonymisation of the data, features such as `medical_history`, `pre-op_medication`, `symptom`, and `lab_result` have been left vague intentionally. This makes it challenging to apply any domain-specific knowledge into the creation of interaction features. As for `symptom` and `lab_result`, it is uncertain at what point during the patient's hospital stay was the information captured. This [study on the factors affecting healthcare costs](https://pubmed.ncbi.nlm.nih.gov/18387070/) acknowledged that hospitalisation costs are the summation costs of various utilised resources which would include drugs, medical supplies, and lab tests. In this instance, it would be beneficial to know the number of medications served and the number of lab tests done for each patient.

#### 3. Limited data on recurring hospitalisations

Of the 3,400 rows in the dataset, 3,000 rows were first-time admissions and 400 rows were repeating admissions. To better study the effect of recurring hospitalisations on bill amount, more data on repeating admissions would be needed. There are 2 features that were engineered to investigate this effect: `days_hospitalised` and `days_since_last_hospitalisation`. However, they had to be dropped eventually due to their low variance since the majority of patients are one-time visitors to the hospital.

### Conclusion

The final lasso regression model has performed well as it is able to explain 97.3% of the total variability in the bill amount with all the features and is generally off-the-mark by 7% on its predictions of the bill amount. It has found the main factors driving cost of care to be `num_of_symptoms`, which is the most important feature predicting bill amount, as well as `race`, `resident_status`, `age_at_admission`, and `weight`, which are among the top few features explaining bill amount.

The future plans for this project could involve extending it to other cities and countries to find the factors driving their cost of care so as to help solve various healthcare problems that are not just limited to the area of health insurance, or adapting it to predict hospital bills at pre-admission by providing patients with up-front cost estimates to help reduce bill shocks and payment challenges after treatment.

### References

[1] https://www.dbs.com.sg/personal/articles/nav/protection/guide-health-insurance-singapore-medishield-medisave?pid=sg-dbs-pweb-insure-product-firstinsurance-image-textlink-medishield-medisave<br>
[2] https://www.dbs.com.sg/personal/articles/nav/protection/integrated-shield-plans<br>
[3] https://www.straitstimes.com/singapore/health/moh-welcomes-measures-by-insurers-to-adjust-terms-for-full-rider-ips-and-require-co<br>