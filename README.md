# HR Insights - Data in Motion Challenge
The best description for this project would be: managing workarounds for things I don't know by using the skills I already have :)<br><br>
This is my very first project in Power BI being also my first practical contact with this tool.<br>
I decided to learn-by-doing and recreate a dashboard I previously made in Tableau.

Contents:
* [The project](#the-project)
* [The data](#the-data)
  <br>
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
- setting appropiate data types etc.<br>

As I decided to focus on information about employees leaving the company, I wanted to find a percentage of people leaving from all departments and subdepartments, for each year. It could surely be done in DAX, but since I was a Power BI newbie, I had to find some other way. My solution was to load the table to BigQuery and use SQL to find the values. 
<br>
So, here's the query showing the number of employees working in each department and subdepartment in each year. Luckily the GoogleSQL syntax is only slightly different from the typical SQL (note the EXTRACT function).

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
I also wanted a number of employees that left every year, but this time I simply made a table visualization with the values I needed and exported it to CSV file. Then it was just a few clicks to join it all in Power Query and add a calculated column to give me the values I was looking for.<br>
I'm sure I'll soon learn to do it all with DAX expressions, but I think my solution works fine as long as all the values are correct.<br>
<br>
