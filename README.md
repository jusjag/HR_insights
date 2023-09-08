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
Data preparation included steps like:
- deleting columns that are unnecessary or even illegal for the employer to store (race, orientation, marital status)
- deleting columns I knew I wasn't going to use (age, IDs of higher level managers)
- setting appropiate data types

Now, I wanted to check the percentage of employees leaving in scale of year or department. It would probably be possible with some advanced DAX expression, but since I was a Power BI newbie, I had to find it other way. I decided to use SQL and loaded the table to BigQuery. Even though it uses slightly different syntax, I appreciate its fast and easy process of importing CSV files. 
<br><br>
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
  count(employee_id) as active_workers
  FROM years
WHERE hire_year <= 2022 AND (term_year >= 2022 OR term_year is null)
group by department, sub_department
```
Could it be done in better way, covering all years in one query? I think so. Did i know how to do it? Not yet :)
<br><br>
I also wanted a number of employees that left every year divided by department and subdepartment. To do so, I simply created a table visualisation in Power BI, exported it to CSV, joined with results of previous query... and voila, finally I could add a calculated column to find the metric I was looking for. 
<br><br>
One day I'll be able to do it all in one or two complex DAX expressions. For now, I think my way also worked fine.<br>

## Step 2: visualisations
## Step 3:
