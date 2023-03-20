# HR ANALYTICS IN POWER-BI
## The core goal of this case study is to build a report using fictitious datasets from a Tech company called Atlas Labs. Atlas Labs HR team wants to be able to monitor key metrics on employees and their secondary goal is to understand what factors impact employee attrition.
LOADING CSVs FILES

The first step when working with power bi is
-  Loading and preparing our dataset.
- Renaming our table to FACT OR DIM for easy identification
- Reviewing the loaded tables and ensuring that the columns are correctly formatted as text, numbers, and dates where expected.
- Modeling data is a major pillar of power bi report development as it enables us to connect different tables together. we will be connecting our six tables together with both active and inactive relationships.
- A dedicated DATE table is highly recommended for accurate date and time reporting.

The Dataset contains Fact table and Dimension tables

The Fact table stores the Performance Ratings. This table contains information about employee’s yearly reviews and helps Atlas Labs manage their employee’s performance on a regular basis. It contains 11 different columns and 6709 rows per employee. While the Dimension table enables us to provide more context to the data - the who, what, when, where, and why. We have 4-dimension tables that we will be working with: Employee, EducationLevel, RatingLevel, SatisfiedLevel, and we will be creating the date table for our future analysis and it will contain detailed information such as year, quarter, month, and day. Altogether we will be working with 5-dimension table and 1 fact table. (image the six table)

Calculated Date Table using DAX code:
