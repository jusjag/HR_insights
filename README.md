# HR Insights - Data in Motion Challenge
The best description for this project would be: <br>
managing workarounds for things I don't know by using the skills I already have :)<br><br>
This is my very first project in Power BI being also my first practical contact with this tool. I decided to learn-by-doing and recreate a dashboard I previously made in Tableau. 

## The project
General project purpose: learn how to use Power BI in practice<br>
Project idea: Visualization challenge "People analytics" from <a href="https://d-i-motion.com/courses/data-viz-challenges/#learndash-course-content">Data in Motion.</a>.<br>
Objective: show insights from a given dataset (challenge description is now locked to logged-in users only, so I don't remember exact requirements).<br>
Dataset: <a href="https://docs.google.com/spreadsheets/d/1Dg_aczyeCh0izhIrZhVDCfuKqSApjMCV7flxaY6iUnA/edit#gid=423853547">see raw table in Google Sheets</a>.
Tools used: PowerBI, PowerQuery, BigQuery, SQL.

## The data:
Data preparation:
- deleting columns that are unnecessary or even illegal for the employer to store (race, orientation, marital status),
- deleting columns I knew I wasn't going to use (age, IDs of higher level managers),
- setting appropiate data types etc
<br><br>
As I decided to focus on information about employees leaving the company, I wanted to find a percentage of people leaving for ach department, subdepartment and year.<br> It's probably possible by using one DAX expression, but since I was a Power BI newbie, I had to find it some other way. My solution was to load the table to BigQuery and use SQL to find the values. 
<br><br>
Here's the query returning number of employees working in each department and subdepartment in each year. Luckily the GoogleSQL syntax is only slightly different from the SQL I use (note the EXTRACT function). 
```sql
WITH years AS
(SELECT
  employee_id,
  department,
  sub_department,
  EXTRACT(year from hire_date) AS hire_year,
  EXTRACT(year FROM term_date) AS term_year
FROM HR_insights.EMP)
SELECT 
  "2022" as year,
  department, 
  sub_department, 
  count(employee_id) as active_workers
  FROM years
WHERE hire_year <= 2022 AND (term_year >= 2022 OR term_year is null)
group by department, sub_department
```
Could it be done in better way, covering all years in one query? I think so. Did i know how to do it? Not yet :)
<br><br>
I also wanted a number of employees that left every year, divided by department and subdepartment. To do so, I simply created a table visualisation in Power BI, exported it to CSV, joined with results of previous query... and voila, finally I could add a calculated column to find the metric I was looking for. 
<br><br>
One day I'll be able to do it all in one or two complex DAX expressions. For now, I think my way also worked fine.<br>

## Step 2: visualisations


## Step 3:
