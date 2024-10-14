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

### Tools
SQL - Data cleaning and analysis

Excel - Creating Report

### Methodology
#### Data cleaning 
- Removing the duplicate, the initial rows is 22,227 after removing the duplicate final query have 22214 rows which mean they are 13 duplicates
- Standardizing the categories variable in our gender column which I changed the FM as ‘Female’, M as ‘Male’.
- Correcting the misspelt words in the dataset, I found some misspelt words in job title (‘Relationshiop’,’Associate Profssor’,’ Assistant Profssor’,’ Coordiate’).
- Formatting the date in the termdate separating the date from the time in the termdate, I added a new column (termdate_only) with the date data type
- Getting the age from the birthdate and hire age from hire date.

  #### Exploratory Data Analysis
 - Calculating tenure at which the employee has used before leaving the company and created a status column to identify the employee who are still active or left.
- Also group the age in three forms based on the actual range of age in the dataset so as to use it for analysis where 22-30 is mid-Adult, 31-45 is Adult, 46-60 is old and the Average age is 41.
- Calculating the total number of employees which is 22214, the total number employee that left which is 3929 and the total number active employees is 18285.

  #### Statistical Analysis
  Descriptive Analysis was used in this analysis to summarize and described the attrition rate across different demographic groups (gender, race, and age) and summarize attrition rated across job related factors, I used it to analyze all my objective questions.

  ### Data Analysis
 - The attrition rate by gender – This analysis will help understand whether one gender has a highest rate of leaving the company compare to others, which can be critical for identifying potential demographic issues related to employee attrition.  The methodology used for this analysis, the fields used in the analysis, such as gender, status of _employee, attrition rate.
Note: Attrition rate is calculated by number of employees who left divided by total number of employees multiply by 100.  Also, the attrition rate was applied separately for each gender category (Male, female, non-conforming) to calculate their respectively attrition rate.

```sql query
SELECT gender, 
 COUNT (*) AS total_employee,
  SUM (CASE WHEN status_of_employee ='LEFT' THEN 1 ELSE 0 END) AS employee_left,
CAST(ROUND(SUM(CASE WHEN status_of_employee = 'LEFT' THEN 1 ELSE 0 END) * 100.0/COUNT (*), 2) AS decimal(5,2))
 AS attrition_rate_by_gender
 FROM NEW_HR_DATA
 WHERE gender IN ('Female','Male','Non-Conforming')
 GROUP BY gender
 ORDER BY gender;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/765eaad5-3235-4d8a-ba4c-18e099517167)
![image](https://github.com/user-attachments/assets/f67ce9e9-2e77-41d7-a374-3b4dee63dc32)
##### Key insight
The analysis indicates that female employees have the highest attrition rate compared to their male and non-conforming counterparts. This trend suggests potential gender-specific challenges within the workplace, such as disparities in work-life balance, career advancement opportunities, or job satisfaction. Such issues could be driving higher turnover among female employees.

- The attrition rate by race – This analysis is to determine the attrition rate by race, understanding how attrition differs among racial group are disproportionately leaving the company, which can be important for assessing diversity and inclusion efforts, The field involved are race, status of employees and attrition rate.
  
```sql
SELECT race,
 COUNT (*) AS total_employee,
 SUM (CASE WHEN status_of_employee ='LEFT' THEN 1 ELSE 0 END) AS employee_left,
CAST(ROUND(SUM(CASE WHEN status_of_employee = 'LEFT' THEN 1 ELSE 0 END) * 100.0/COUNT (*), 2) AS decimal(5,2))
 AS attrition_rate_by_race
 FROM NEW_HR_DATA
 WHERE race IN ('Asian’, ‘Two or More Races', ' American Indian or Alaska Native', 'Black or African American', ' White', ' Hispanic or Latino')
 GROUP BY race
 ORDER BY;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/e9bb73cd-0cb5-4338-afab-73bf489d9d10)
![image](https://github.com/user-attachments/assets/83c86942-f931-43af-87da-3a4f1aceb960)
##### Key insight
The analysis of attrition by race shows that employees identifying as ‘Native Hawaiian or Other Pacific Islander’ Races have the highest turnover rate, while Black and Asian employees share the same, lower attrition rate. This indicates that employees from diverse racial backgrounds, particularly those identifying with more than one race, may face challenges in the workplace that contribute to higher turnover. These challenges could stem from feelings of exclusion, lack of representation, or cultural mismatches within the company.

-	The attrition rate by age group- The goal of this analysis is to determine the attrition rate across different age groups. Understanding how age impacts employee turnover, it also helps to identify whether specific age demographic is more likely to leave the company this information can be used to tailor retention strategies that address the needs of different age group. The specific field involve such as birth date, status of employees, also used the birth date to calculate the age of the employees and group them into categories, where from 22- 30 years old are categorize as mid-Adult, 31-45 years old as adult and 46-60 as old. The grouping allows to assess the attrition rate within each age group.

```sql
SELECT age_group,
 COUNT (*) AS total_employee,
 SUM (CASE WHEN status_of_employee ='LEFT' THEN 1 ELSE 0 END) AS employee_left,
CAST(ROUND(SUM(CASE WHEN status_of_employee = 'LEFT' THEN 1 ELSE 0 END) * 100.0/COUNT (*), 2) AS decimal (5,2))
 AS attrition_rate_by_age_group
 FROM NEW_HR_DATA
 WHERE age_group IN ('Mid-Adult’, ‘Adult', 'Old')
 GROUP BY age_group
 ORDER BY age_group DESC;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/703f6d7a-aedc-443e-8d5c-6ec56146e394)
![image](https://github.com/user-attachments/assets/caa27022-50da-4ff6-98cc-791fa825ba1e)
##### Key insight
From this analysis indicates that mid-adults (22-30 years) experience the highest attrition rate within the organization, the next highest attrition rate is observed among adults (31-45 years), Old employees (46-60 years) show the lowest attrition rate, indicating stronger retention within this group. This pattern suggests that younger employees may face challenges related to career development, job satisfaction, or work-life balance that prompt them to leave earlier in their careers. In contrast, older employees, who may be more settled in their roles, are less likely to leave.
 
-	The attrition rate by department- The of the analysis is to calculate the attrition rate across different department. This help identify whether certain department have higher employees’ turnover which could point to issues such as job dissatisfaction, management challenges or work over load distribution The field involve is department, status of employee and attrition rates.
``` sql
SELECT department,
 COUNT (*) AS total_employee,
 SUM (CASE WHEN status_of_employee ='LEFT' THEN 1 ELSE 0 END) AS employee_left,
 CAST(ROUND(SUM(CASE WHEN status_of_employee = 'LEFT' THEN 1 ELSE 0 END) * 100.0/COUNT (*), 2) AS decimal(5,2))
 AS attrition_rate_by_department
 FROM NEW_HR_DATA
 WHERE department IN ('Engineering','Services','Accounting','Training', 'Sales’, ‘Research and Development’, ‘Business Development','Support',
 'Product Management','Auditing','Marketing', 'Legal’, ‘Human Resources')
 GROUP BY department
 ORDER BY attrition_rate_by_department desc;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/d84d8281-babc-4c19-8da5-b7ae97546926)
![image](https://github.com/user-attachments/assets/52c7561d-993b-4f97-9f34-712eaec35b68)
##### Key insight
High turnover in the Auditing department may indicate issues such as job dissatisfaction, high stress levels, or limited career progression opportunities within this specific area. Similarly, high attrition in the Legal, Research department could suggest challenges with job engagement, workload, or professional development.

-	The attrition rate by job title – this analyzing helps identify roles with the highest turnover, revealing potential issues such as job dissatisfaction, lack of career growth, or workload imbalance. This insight allows organizations to target specific positions with retention strategies, improving employee satisfaction and reducing costly turnover.
``` sql
WITH employee_counts AS (
 SELECT jobtitle, 
 COUNT(*) AS total_employee,
 SUM(CASE WHEN termdate_only IS NOT NULL THEN 1 ELSE 0 END)
 AS employee_left
 FROM NEW_HR_DATA 
 GROUP BY jobtitle)
 SELECT jobtitle, total_employee, employee_left,
 CASE WHEN total_employee > 0 THEN
 CAST(ROUND ((employee_left * 100.0 /total_employee),2) AS DECIMAL (5,2))
 ELSE 0
 END AS attrition_rate_by_jobtitle
 FROM employee_counts
 ORDER BY attrition_rate_by_jobtitle DESC;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/bfb0f6ac-1856-4b33-ae42-2b94fcac7a3b)
![image](https://github.com/user-attachments/assets/88d109ff-5d18-4359-b184-9bf3c0d143e3)
##### Key insight
The key insight from this analysis shows that Official Assistant, Statistician, and Executive Secretary have the highest attrition rates among the top 10 job titles. This suggests that employees in these roles may face specific challenges, such as limited career advancement, high workload, or dissatisfaction with job responsibilities. This high turnover could be due to factors such as job monotony, limited opportunities for advancement, or job dissatisfaction. Roles that involve repetitive tasks or lack career growth may lead employees to seek opportunities elsewhere, contributing to higher attrition in these positions.

- The attrition rate by location - Analyzing attrition rates at headquarters versus remote locations reveals differences in employee retention based on work environment. This insight helps organizations understand if remote work offers better flexibility and satisfaction or if headquarters roles face unique challenges, enabling more effective retention strategies tailored to each work setting.

  ```sql
  WITH employee_counts AS (
 SELECT location,
 COUNT (*) AS total_employee,
 SUM (CASE WHEN termdate_only IS NOT NULL THEN 1 ELSE 0 END)
 AS employee_left
 FROM NEW_HR_DATA 
 GROUP BY location)
 SELECT location, total_employee, employee_left,
 CASE WHEN total_employee > 0 THEN
  CAST (ROUND ((employee_left * 100.0 /total_employee),2) AS DECIMAL (5,2))
 ELSE 0
 END AS attrition_rate_by_location
 FROM employee_counts
 ORDER BY attrition_rate_by_location DESC;
```

  


  







