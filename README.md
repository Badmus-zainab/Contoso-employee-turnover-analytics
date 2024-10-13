# Contoso Employee Turnover Analytics

## Insights And Solutions for Retention

### Project Overview
Contoso company has been facing employee turnover, where the HR department reach out to me and provide a dataset containing the information on employee demographic, job roles, races and termination date, hire date, gender. The company offers working from Headquarter and remotely.
![Screenshot_24](https://github.com/user-attachments/assets/d9857258-3514-4b50-8ba9-353cda533fc9)
![Screenshot_25](https://github.com/user-attachments/assets/4fb881e6-32ef-4b9d-b13e-ea40abaf59bb)

### Problem Statement
Identifying key factors contributing to employee attrition and how it can be solved.

### Problem Objective
-	Demographics factors: Which gender, races and age group has the highest attrition rate?
-	Job related factors: Determine which department, job title, tenure are most strongly associated with higher employee attrition?
-	Location based trends: Are there difference in attrition rates between different location headquarters vs Remote?
-	How do city and state locations impact employee attrition?
-	Tenure analysis: How does the length of employment (tenure) correlate with attrition?
-Is there a critical point at which attrition splices (like employees leaving after 1-2 years)?
-	Hiring and Termination trends: What trends can be observed in their period of high turnover?
-Is there difference in retention between employees hired more recently versus those with longer tenure?

### Data Description
- Data source: The Data Initiatives
- Data collection: EXCEL file
- Data characteristics:  ID – Unique identifier for each employee record
- First_name – The first name of the employee
- Last_name – The last name of the employee
- Birthdate – The birth date of the employee
- Gender- The gender of the employee
- Races – The race or ethnicity of the employee
- Department – The department where the employee works
- Location- The office of work location of the employee
- Hire_date – The date the employee was hired by the company
- Termdate (Termination date) – The date the employee left or was terminated from the company
- Location_city - The city where the employee work location is based
-Location_state – The state where the employee work location is based.

### Methodology
#### Data cleaning 
- Removing the duplicate, the initial rows is 22,227 after removing the duplicate final query have 22214 rows which mean they are 13 duplicates
- Standardizing the categories variable in our gender column which I changed the FM as ‘Female’, M as ‘Male’.
- Correcting the misspelt words in the dataset, I found some misspelt words in job title (‘Relationshiop’,’Associate Profssor’,’ Assistant Profssor’,’ Coordiate’).
- Formatting the date in the termdate separating the date from the time in the termdate, I added a new column (termdate_only) with the date data type
- Getting the age from the birthdate and hire age from hire date.







