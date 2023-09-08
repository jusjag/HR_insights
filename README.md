# HR Insights - Data in Motion Challenge
The best description for this project would be: managing workarounds for things I don't know, using the skills I already have.<br>
This is my very first project in Power BI being also my first practical contact with this tool. I already had some Tableau experience but zero knowledge of DAX, which would cetrainly help me. So I had to find other way to do all the things I wanted.<br>
<b>But this is exactly what makes me a great data analyst: I look for solutions.</b> I search for answears. I don't give up because of a sigle error (or a two-day string of errors either). 
<br><br>
General project purpose: learn how to use Power BI in practice<br>
Data source: Data in Motion Challenge<br>
Challenge objections: 
Tools used: PowerBI, PowerQuery, BigQuery, Figma

## Step 1: the data
Full dataset can be found here:
- deleting columns that are unnecessary or even illegal for the employer to store (race, orientation, marital status)

## Step 2: Visual analysis

## Step 3: Some SQL
Next, I wanted to know the percentage of people leaving compared to all active workers from all departments and subdepartments. The departments vary significantly by size, so the absolute numbers don't show the real picture.<br> 
Since I was new to Power BI and didn't know DAX very well, I decided to use SQL.<br>
The fastest way was using BigQuery. Pros: fast and easy process of uploading and querying a CSV file. Cons: BQ has a slightly different SQL syntax, for example EXTRACT(year from date) instead of year(date). 
So the query below gives information about active and gone employees from every department and subdepartment, for every year. 
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
  count(employee_id) as active_workers,
  count(term_year) as gone
  FROM years
WHERE hire_year <= 2022 AND (term_year >= 2022 OR term_year is null)
group by department, sub_department
```
Could it be done in better way, covering all years in one query? I think so. Did i know how to do it? Not yet :) I'm sure I'll go back to this query later because it 
