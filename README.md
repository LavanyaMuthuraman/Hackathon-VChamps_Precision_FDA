# Hackathon Challenge
## [V-Champs_Precision_FDA](https://precision.fda.gov/challenges/31) (The Veterans Cardiac Health and AI Model Predictions Challenge)

![aii1](https://github.com/LavanyaMuthuraman/Hackathon-VChamps_Precision_FDA/assets/109660074/60c3da65-310b-42b1-85dc-f108d1dfea84)

To develop and evaluate (AI/ML) models to predict cardiovascular health related outcomes in Veterans. Primary outcome of interest: 
1. All-cause mortality
2. Mortality for Cardiovascular 
3. Hospital readmission for all causes
4. Hospital readmission for Cardiovascular

### **Data**

There are 16 CSV files provided for this challenge: Train, Test, Quality_Check.

- **We have done analysis for all 16 CSV files, based on the analysis we have skipped these files.**

Inpatient location,
Inpatient specialty,
Demographic event,
Demographic Static,
Medication_ordered,
Medications_administered,
Ed_visit,
Outpatient_visit and
Procedures.

- **Only we took these below high potential files.**

Inpatient admission,
Conditions,
Immunization,
Lab results,
Measurements and
Measurements blood pressure.

### **Feature Engineering:**

- To begin with, We have done Explanatory analysis for all 16 CSV files, based on the analysis we only took the high potential files that relevant to the objective.  
During the exploratory phase, we noticed that there were numerous records for a single patient across various time periods. To tackle this, we rounded off the ages to one, two, or three decimal places, and subsequently applied the 'Max' condition to the age column.
- By using the 'Max' condition, we isolated the most recent record for each patient. However, in the latest record, we still encountered multiple values for some patients. To streamline the data further, we merged the age and potential columns with underscores. Subsequently, we grouped the data by 'Internal patient id,' effectively resulting in only one latest record for each patient. 
- After performing transformations on each file, we merged them with the 'Death' file to create a single data frame. In this data frame, we separated the data into three categories: Textual, Numerical, and Target. For the Textual columns, we utilized the sentence transformer technique to convert words into vectors, allowing for efficient analysis of the text data. As for the Numerical columns, we applied the Standardization technique to scale the data, ensuring a common range and aiding in better model performance.

### **Generating Readmission Target CSV file:**

- To generate the Readmission Target CSV file, we analyzed the 'Inpatient admissions' file by examining the occurrences of each patient using the 'Internalpatientid' column. Based on this analysis, we created a new column where we assigned a value of 1 if a patient had more than one occurrence and 0 if they had exactly one occurrence. This process enabled us to generate the target column for readmission prediction.
- For the readmission prediction, we considered high-potential files such as 'Condition', 'Lab results', 'Measurements blood pressure', 'Immunization', and 'Measurements'. Additionally, we included the 'Inpatient admissions' file. We applied similar transformations to these files as we did for the mortality prediction.

### **Generating Cardiovascular/Non-Cardiovascular CSV file:**

- To segregate Cardiac and Non-cardiac patients, we used the 'Condition code icd10 subcategory' column from the 'condition' file. By conducting a word search caping using the disease names mentioned in the PrecisionFDA document.
- And then we classified patients into two distinct groups: Cardiac (1) and non-cardiac (0) patients.
  
### **Model Building:**

- After feature engineering, we trained the transformed data using multiple base models (Random Forest Classifier, Support Vector Classifier, XG Boost Classifier, Bi-LSTM, etc.,). The **XGBoost Classifier**, with the highest accuracy, was selected initially without hyperparameter tuning. Later, hyperparameter tuning was performed using Bayesian search cv to find the optimal parameters for the model.

- As a result, the metrics presented on the challenge page were generated using the XG Boost model.

![image](https://github.com/LavanyaMuthuraman/Hackathon-VChamps_Precision_FDA/assets/109660074/c03afbb0-21c8-481e-928f-3756b4ade377)
![image](https://github.com/LavanyaMuthuraman/Hackathon-VChamps_Precision_FDA/assets/109660074/f7479a56-3173-4dde-9d87-2324e2c155a7)
