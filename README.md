# HR ANALYTICS IN POWER-BI
## Introduction 

The core goal of this case study is to build a report using fictitious datasets from a Tech company called Atlas Labs. Atlas Labs HR team wants to be able to monitor key metrics on employees and their secondary goal is to understand what factors impact employee attrition.

LOADING CSVs FILES

The first step when working with power bi is

-  Loading and preparing our dataset.
- Renaming our table to FACT OR DIM for easy identification
- Reviewing the loaded tables and ensuring that the columns are correctly formatted as text, numbers, and dates where expected.
- Modeling data is a major pillar of power bi report development as it enables us to connect different tables together. we will be connecting our six tables together with both active and inactive relationships.
- A dedicated DATE table is highly recommended for accurate date and time reporting.

The Dataset contains Fact table and Dimension tables

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/hr%20dataset.png)

The Fact table stores the Performance Ratings. This table contains information about employee’s yearly reviews and helps Atlas Labs manage their employee’s performance on a regular basis. It contains 11 different columns and 6709 rows per employee. While the Dimension table enables us to provide more context to the data - the who, what, when, where, and why. We have 4-dimension tables that we will be working with: Employee, EducationLevel, RatingLevel, SatisfiedLevel, and we will be creating the date table for our future analysis and it will contain detailed information such as year, quarter, month, and day. Altogether we will be working with 5-dimension table and 1 fact table.

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/6%20tables.png)

Calculated Date Table using DAX code:

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/dim%20table.png)

## Data Model Connection

In the FactPerformanceRating table,
we have four different types of performance ratings: 
- EnvironmentalSatisdfaction, 
- JobSatisfaction,RelationshipSatisfaction, and 
- WorkLifeBalance 

All these have numbers from 1-5 but we have no context of what these ratings mean. connecting them will help us with our analysis.

- connect our DimDate table to the FactPerformanceRating table
- connecting the DimEducationLevel table to the DimEmployee table
- connecting DimSatisfactedLevel and using EnvironmentalSatisdfaction as the active relationship
- connecting DimRatingLevel and using SelfRating as the active relationship

![Data model: Snowflake schema](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/data%20model.png) 

## Exploring the Data

The leadership team at Atlas Labs is looking to have visibility on high-level metrics about the state of its employees. In particular, the organization is looking to understand the attrition at the company.

## STEP 1

- Created an overview page
- Created a new table called _Measures
- Calculated TotalEmployees inside the _Measure table which count all employees.
- Calculated ActiveEmployees and InactiveEmployees, which take count of all currently active and inactive employees.
- Calculated % Attrition Rate using ActiveEmployees and InactiveEmployees measures. The attrition rate for Atlas Labs is 16.1%.

## Hiring trends over time

The head of HR has requested for a report to be created that enables them to have a view of the whole organization’s key metrics, this will enable them to benchmark their HR metrics against organizations across their industry as well as understand how their employees are performing.  They would like to start by analyzing their hiring trends over time to see where they see the biggest growth in new employees.

- Created a new measure called TotalEmployeesDate to help us view TotalEmployees by Date in our visual

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/employee%20hiring%20trand.png)

INSIGHT - Of all employees hired in 2021, 116 are still with the organization.

## Analyzing departments and jobs

The HR team is working with department managers to understand their teams and what type of typical roles they are hiring into the organization, this will enable every department to plan for new hiring requests in the future.

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/active%20employee%20by%20dept.png)

INSIGHT: Technology have a total of 828 active employees by the department while HR has just 51

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/active%20employee%20by%20dept%2Cjobrole.png)

INSIGHT: software engineer has a total number of 247 active employees under Technology.

## AN OVERVIEW OF ATLAS LAB DASHBORD

![OVERVIEW DASHBOARD](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/overview.png)

## Demographics: Age and Gender

Let’s look at the next layer of key HR metrics that focus on Diversity and Inclusion. We will create a new page for this analysis called “Demographics”

- Created a visual to display minimum and maximum values for Age. 

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/age.png)

- Created a chart to view TotalEmployees by AgeBins. 

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/employee%20by%20agebins.png)

- Created a chart to view Totalemployees by AgeBins and Gender 

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/employee%20by%20agebin%20n%20gender.png)

Added a page-level filter that enables us to look at the report base on active or inactive employees.

## Demographics: Marital status and Ethnicity

- Created a chart to display the count of all employees by Marital Status. 

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/marital%20status.png)

- Created an AverageSalary measure which gives the average salary of all employees.

- Created a chart to display the count of all employees and their average salary and Ethnicity.

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/avg%20salary%20and%20ethnicity.png)

## A DEMOGRAPHICS VIEW OF ATLAS LAB DASHBORD

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/demographics.png)

## STEP 2

Created a Performance Tracker page

HR team would like to have a view where they can continually track an individual employee’s performance scores based on their yearly performance reviews.

- Created a calculated column FullName which combines FirstName and LastName in our DimEmployee table.

- Created a slicer that will be able to filter the report page based on the employee’s FullName.

- Created a visual that displays the selected employee’s HireDate and renamed it as Start Date

- Created a measure LastReviewDate that gets the last performance review for the selected individual and displayed it on a visual as Last Review.

- Created a measure NextReviewDate that calculates when the next review is due, which should be 365 days after the LastReviewDate, and displayed it on a visual as Next Review.

## Individual review rating

- Created a JobSatisfaction measure inside the _Measure table, which works out the max FactPerformanceRation[JobSatisfaction] level. Thou other three satisfaction metrics do not currently have an active relationship to DimSatisfiedLevel, I activated it by creating 3 new measures EnivironmentalSatisfaction, RelationshipSatisfaction,a and WorkLifeBalance using the USERELATIONSHIP() function.

- Created a visual to display EnivironmentalSatisfaction, RelationshipSatisfaction,a and WorkLifeBalance by year. 

- Created 2 more measures SelfRating and ManagerRating that provide the max rating ID, using USERELATIONSHIP() function.

- Created a visual to display SelfRating and ManagerRating by year.

## A PERFORMANCE TRACKER OF ATLAS LAB DASHBORD

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/performance%20tracker.png)

## Insights on Estelle

We've uncovered some interesting insights about Estelle Chung. We can see that the managerial rating level and self-performance level don't always align and that most recently, Estelle received a "Needs improvement" rating.

We advise the HR/management team to Organize a meeting to discuss needs and create an improvement plan in order to support Estelle's growth and ensure she’s retained.

## Employee Attrition

## Note- Employee attrition or churn or turnover refers to when an employee leaves an organization for any reason. (Voluntary or involuntary)

-Created a visual to display the attrition rate for each department and job role.

We would like to understand our attrition rate based on our HireDate. First created a measure that uses CALCULATE () on our InactiveEmployees and makes use of the USERELATIONSHIP () function naming this measure as InactiveEmployeeDate. Also created a measure that calculates the rate of attrition based on InactiveEmployeeDate and TotalEmployeesDate, naming it attrition Rate Date.

-Created a visual that displays attrition rate date over time naming it Attrition by Hire Date.

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/hire%20date.png)

-Created a visual that displays attrition rate by job role and department.

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/job%20role%20and%20dept.png)

INSIGHT- Sales-sales representative has the highest attrition rate of 39.8% despite being one of the smaller job role groups in the organization.

-Created a visual to display the Attrition Rate and TotalEmployees for Business Travel renaming it Attrition by Travel Frequency

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/travel%20frquency.png)

INSIGHT- Employees who were considered frequent travelers had the highest attrition rate of 24.9% despite only making up 19% of the total hires. Perhaps the frequency of travel became an issue for some of the employees and led to them leaving the organization.
Recommendation- Review travel requirement policy and survey employees on feelings around travel frequency. Getting employee feedback will be a great way to determine whether this is impacting employee happiness.

-Created a visual to display the Attrition Rate based on years working for Atlas Lab renaming it as Attrition by Tenure.

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/tenure.png)

## AN ATTRITION VIEW OF ATLAS LAB DASHBORD

![](https://github.com/okonkwoloretta/HR-analysis-in-Power-BI/blob/main/attrition%20dashboard.png)

## Overall Key insights 

- Atlas Labs has employed over 1470 people
- Atlas Labs currently employs 1200 people
- The largest department by far is technology
- The attrition rate for employees leaving the organization is 16%
- The majority of employees hired at Atlas Labs are between the ages of 20 and 29 years old
- Active employees, women make up 2.7% of the organization
- Employees who identify as non-binary make up 8.5% of total employees
- Employees who identify as white have the highest average salary despite making up the majority of the organization
- Employees who identify as mixed or multiple ethnic groups have one of the lowest average salaries


Thank you for sticking by me and getting to this point. 

