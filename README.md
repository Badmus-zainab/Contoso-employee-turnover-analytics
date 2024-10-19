# Contoso Employee Turnover Analytics
## Insights And Solutions for Retention

## Table of contents
- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Problem Objectives](#problem-objectives)
- [Data Desription](#data-description)
- [Tools](#tools)
- [Methodology](#methodology)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Statistical Analysis](#statistical-analysis)
- [Data Analysis](#data-analysis)
- [Conclusions](#conclusions)
- [Recommendations](#recommendations)
  
### Project Overview
Contoso company has been facing employee turnover, where the HR department reach out to me and provide a dataset containing the information on employee demographic, job roles, races and termination date, hire date, gender. The company offers working from Headquarter and remotely.
![Screenshot_24](https://github.com/user-attachments/assets/d9857258-3514-4b50-8ba9-353cda533fc9)
![Screenshot_25](https://github.com/user-attachments/assets/4fb881e6-32ef-4b9d-b13e-ea40abaf59bb)

### Problem Statement
Identifying key factors contributing to employee attrition and how it can be solved.

### Problem Objectives
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
WITH employee_counts AS ( SELECT location,COUNT (*) AS total_employee, SUM (CASE WHEN termdate_only IS NOT NULL THEN 1 ELSE 0 END) AS employee_left FROM NEW_HR_DATA
GROUP BY location)SELECT location, total_employee, employee_left, CASE WHEN total_employee > 0 THEN
CAST (ROUND ((employee_left * 100.0 /total_employee),2) AS DECIMAL (5,2))ELSE 0END AS attrition_rate_by_location
FROM employee_countsORDER BY attrition_rate_by_location DESC;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/c282cf58-a04c-4d9b-8ec5-700701c82102)
![image](https://github.com/user-attachments/assets/cc1dc107-b747-4630-a771-35bdbb7f4c4c)
##### Key insight
This may indicate that employees working at the headquarters face more stress or challenges compared to their remote counterparts. Headquarters employees might deal with longer commutes, office politics, or a stricter work environment, leading to higher dissatisfaction and, consequently, higher attrition. In contrast, remote employees may enjoy more flexibility and work-life balance, resulting in lower turnover.

- The attrition rate by location in city - Analyzing attrition rates by city location helps identify geographic areas with higher employee turnover. Understanding these differences allows organizations to tailor retention strategies to address the unique needs of employees in different cities.

 ```sql
WITH employee_counts AS (
 SELECT location city, 
 COUNT (*) AS total_employee,
 SUM (CASE WHEN termdate_only IS NOT NULL THEN 1 ELSE 0 END)
 AS employee_left
 FROM NEW_HR_DATA 
 GROUP BY location_city)
 SELECT location_city, total_employee, employee_left,
 CASE WHEN total_employee > 0 THEN
 CAST (ROUND ((employee_left * 100.0 /total_employee),2) AS DECIMAL (5,2))
 ELSE 0
 END AS attrition_rate_by_location_city
 FROM employee_counts
 ORDER BY attrition_rate_by_location_city DESC;
 ```
 #### Report/Visuals
 ![image](https://github.com/user-attachments/assets/a60e45b9-36d7-4ac6-985a-b5d6fca9c5c4)
![image](https://github.com/user-attachments/assets/d02b639c-ebfd-43b5-812d-7b8fbc9530bc)
##### Key insight
High attrition in specific locations can indicate underlying issues such as unfavorable working conditions, lack of local resources, or a disconnect between the company's culture and the local workforce. Employees in these locations may also face longer commutes, limited access to amenities, or less competitive compensation compared to other regions, contributing to their decision to leave.

-	The attrition rate by location state - Analyzing attrition rates by state location helps identify geographic areas with higher employee turnover. Understanding these differences allows organizations to tailor retention strategies to address the unique needs of employees in different states.

```sql
WITH employee_counts AS (
 SELECT location_state, 
 COUNT (*) AS total_employee,
 SUM (CASE WHEN termdate_only IS NOT NULL THEN 1 ELSE 0 END)
 AS employee_left
 FROM NEW_HR_DATA 
 GROUP BY location_state)
 SELECT location_state, total_employee, employee_left,
 CASE WHEN total_employee > 0 THEN
 CAST (ROUND ((employee_left * 100.0 /total_employee),2) AS DECIMAL (5,2))
 ELSE 0
 END AS attrition_rate_by_location_state
 FROM employee_counts
 ORDER BY attrition_rate_by_location_state DESC;
 ```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/5553d4ba-2845-433f-811d-dff232517ca2)
![image](https://github.com/user-attachments/assets/88148cd9-c3d4-4926-9dc8-97dada515ba7)
##### Key insight
This indicates that employees in these states may encounter unique challenges especially in Indiana which has the highest attrition rate, such as local economic conditions, workplace dissatisfaction, or lack of growth opportunities. Implementing targeted retention strategies in these states.

-	The employee turnover by tenure - Analyzing attrition rates based on tenure helps identify when employees are most likely to leave, revealing critical points in their career lifecycle. This insight allows organizations to implement targeted interventions, such as enhanced onboarding, mid-career development opportunities, and retention initiatives, aimed at reducing turnover during key stages of employment.

```sql
WITH tenure_counts AS (
 SELECT CASE
 WHEN tenure BETWEEN 0 AND 2 THEN '0-2 years'
 WHEN tenure BETWEEN 3 AND 5 THEN '3-5 years'
 when tenure BETWEEN 6 AND 8 THEN '6-8 years'
 WHEN tenure >8  THEN '9+ years'
 ELSE 'UNKONWN'
 END AS tenure_group,
 COUNT (*) AS total_employee,
 SUM (CASE WHEN termdate_only IS NOT NULL THEN 1 ELSE 0 END)
 AS employee_left
 FROM NEW_HR_DATA
 GROUP BY CASE
  WHEN tenure BETWEEN 0 AND 2 THEN '0-2 years'
 WHEN tenure BETWEEN 3 AND 5 THEN '3-5 years'
 when tenure BETWEEN 6 AND 8 THEN '6-8 years'
 WHEN tenure >8 THEN '9+ years'
 ELSE 'UNKONWN'
 END)
 SELECT tenure_group, total_employee, employee_left
 FROM tenure_counts
 ORDER BY employee_left;
 ```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/75aef0bf-ceaf-4b46-91ed-bd1f29e378cf)
![image](https://github.com/user-attachments/assets/d74ca6a9-1bd4-4c80-be02-71b670ec8b9c)
##### Key insight
This suggests that long-term employees may become disengaged or feel that they have limited career advancement opportunities after a certain period of time. Other potential factors include burnout, dissatisfaction with compensation, or a lack of alignment with the company's direction as it evolves over time. Employees who have been with the company for an extended period may also leave if they feel underappreciated or if they seek new challenges elsewhere.

- The rate of employee turnover by month - Analyzing employee turnover rates by month reveals patterns in when employees are most likely to leave. This insight helps organizations identify seasonal trends, potential workplace issues, or external factors impacting retention, allowing them to plan targeted interventions, improve workforce stability, and proactively address turnover during high-risk periods.

```sql
WITH monthly_attrition AS (
    SELECT 
        DATEPART(MONTH, termdate_only) AS month_number,
        DATENAME(MONTH, termdate_only) AS month_name,
        COUNT(*) AS employees_left
    FROM 
        NEW_HR_DATA
    WHERE 
        termdate_only IS NOT NULL
    GROUP BY 
        DATEPART(MONTH, termdate_only), 
        DATENAME(MONTH, termdate_only)
),
max_attrition AS (
    SELECT 
        MAX(employees_left) AS max_employees_left
    FROM 
        monthly_attrition
)
SELECT 
    ma. month_name, 
    ma.employees_left,
    CASE 
        WHEN ma.employees_left = maxa.max_employees_left THEN 'Highest' 
        ELSE '' 
    END AS max_attrition_flag
FROM 
    monthly_attrition ma
CROSS JOIN 
    max_attrition maxa
ORDER BY 
    ma.employees_left;
```
#### Report/Visuals
![image](https://github.com/user-attachments/assets/effb103a-3b57-4e4d-8ebd-e523042e500d)
![image](https://github.com/user-attachments/assets/6a639041-333e-4392-8e61-3c82395927a0)
##### Key insight
August showing the highest attrition rate indicates that the summer months might be a critical period for employee turnover, employees may use mid-year evaluations or performance reviews as a time to evaluate their job satisfaction and explore new opportunities.

### Conclusions
The analysis of attrition rates reveals several critical issues that could impact the company's overall stability and growth if not addressed effectively. 
- The higher attrition rate among female employees highlights a pressing issue in the company's retention strategy. This disparity suggests that female employees may not be receiving the same level of support, career development, or growth opportunities as their male counterparts. If this issue is left unresolved, it could lead to a significant talent gap, diminished diversity within the workforce, and increased recruitment costs over time.
- The higher attrition rate among employees identifying as Two or More Races points to potential issues with inclusivity and support for diverse racial identities. This demographic may face challenges that are not being adequately addressed by the company's current diversity and inclusion efforts. Conversely, the lower turnover rates among Black and Asian employees suggest better retention within these groups. However, this does not necessarily mean that diversity and inclusion efforts are fully effective; it may still be necessary to enhance these initiatives to improve retention across all racial demographics. 
- The higher attrition rates among Mid-Adults and Adults indicate that younger employees, who may represent the future leadership pipeline, are leaving the company more frequently. This could be due to unmet career expectations or a lack of advancement opportunities and failure to address their needs could lead to skill gaps and increased recruitment costs as the company attempts to fill these positions. 
- The elevated attrition rates in the Legal and Research departments suggest that employees in these areas are facing significant challenges that affect their decision to remain with the company. These challenges may include higher stress levels, inadequate support, or insufficient career development opportunities. The company risks losing key talent in these critical departments, which could negatively impact overall performance and innovation. 
- High attrition rates among Official Assistants, Statisticians, and Executive Secretaries indicate that employees in these roles may not be finding sufficient engagement, recognition, or growth opportunities and overload work. The turnover in these positions can disrupt operations and increase the costs associated with hiring and training replacements. 
- The higher turnover rate at the headquarters suggests potential issues with the work environment or employee satisfaction specific to that location. If not addressed, this could lead to increased recruitment and onboarding costs, as well as a loss of institutional knowledge. On the other hand, the lower attrition rates among remote employees indicate that flexibility and a positive work-life balance are effective in retaining talent.
- Elevated turnover rates in Indiana and Ohio highlight that employees in these states are more likely to leave the company, which could adversely affect operations and profitability in these regions. High turnover in these states can result in increased recruitment costs, gaps in institutional knowledge, and disruptions in team dynamics. Addressing the specific factors driving turnover in these locations is crucial for improving retention and stabilizing the workforce in these regions. 
- The high attrition rate among long-tenured employees is alarming because it signifies the loss of experienced workers who possess valuable institutional knowledge. This turnover can disrupt operational continuity and escalate costs related to replacing seasoned staff. Therefore, it is crucial for the company to focus on retaining long-term employees to preserve stability and organizational memory.
- Additionally, the elevated attrition rate observed in August indicates a need for targeted retention strategies during this peak period. Identifying and addressing the underlying causes of turnover in August can prevent further increases in attrition rates.
There is a significant difference in retention between employees hired more recently and those with longer tenure, the company appear to be losing more of its long-term employees indicating burnout or desire for new challenge while recently hired employees are still integrating into the company and are more engaged with their roles.

### Recommendations
To effectively tackle employee turnover, the company needs to implement a series of targeted strategies aimed at improving retention across different groups and locations. Key areas for focus include gathering direct feedback, enhancing diversity and inclusion, and addressing specific departmental and regional challenges.
- Feedback and Support for Female Employees: The company should start by actively seeking direct feedback from female employees to identify specific challenges they face, such as issues related to work-life balance, pay equity, or career advancement opportunities. Develop mentorship and career development initiatives specifically designed to support female employees, fostering their professional growth and increasing retention rates.
Conduct an internal review of existing gender-related workplace policies to ensure they promote an inclusive and supportive environment for all employees.
- Strengthening Diversity and Inclusion: The company should enhance its diversity and inclusion initiatives with a focus on creating a supportive environment for employees of diverse racial backgrounds, including those identifying with multiple races. Establish mentorship programs and employee resource groups that cater specifically to diverse employees and implement ongoing diversity training to foster an inclusive workplace culture.
- Retention Strategies for Younger Employees: Provide opportunities for career growth, mentorship, and clear pathways for advancement and conduct periodic check-ins to address concerns and ensure job roles align with career aspirations, helping employees feel valued and motivated.
- Addressing Turnover in Department: Conduct Surveys and Exit Interviews and use the detailed surveys and exit interviews to identify specific reasons for dissatisfaction. Enhance career progression opportunities, reduce workload stress, and provide additional support and resources and also introduce regular professional development and mentorship programs to engage and retain employees.
- Improving Retention in High-Turnover Roles: Provide opportunities for skill development, job enrichment, and career advancement also, allow employees to take on diverse responsibilities or engage in cross-training for other positions
- Reducing Turnover at Headquarters: Implement Flexible Work Arrangements offer flexible work options similar to those available to remote employees and improve Workplace Environment: Enhance the workplace environment, provide stress management resources, and offer career growth opportunities.
 - Location-Specific Strategies: Conduct Location-Specific Assessments: Review compensation, work conditions, and employee engagement programs in these areas and provide incentives and improve work environments based on specific regional needs.
- Targeted Retention Strategies for Long-Tenured Employees: One such approach is to offer career development opportunities. Even long-tenured employees need to feel that they have room to grow within the company. By providing continuous learning and professional growth programs, organizations can keep these employees motivated and engaged, this could include offering opportunities for advancement, additional training, or new challenges that align with their experience and expertise.
Another effective strategy is to implement mentorship programs. Senior employees can serve as mentors to newer staff, which not only leverages their experience but also strengthens their connection to the company.
Recognition initiatives are also crucial. Acknowledging and celebrating the contributions of long-tenured employees reinforces their value to the company. Regular recognition, whether through formal awards, personalized gestures, or public acknowledgment, can help long-term employees feel appreciated and respected for their ongoing dedication.
- Retention strategy for the peak month: Implement initiatives to keep employees engaged and satisfied throughout the year, especially during the summer months. This could include flexible work options or additional incentives, consider introducing retention bonuses or other rewards for employees who stay through critical periods, such as August.

 By implementing these recommendations, the company can potentially reduce turnover rates and enhance overall employee satisfaction, leading to a more stable workforce.

# THANK YOU
                                                                                



  


  







