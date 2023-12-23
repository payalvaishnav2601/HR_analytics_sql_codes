# HR_analytics_sql_codes

1. Average Attrition Rate for all the Departments. 

SELECT 
department,
Count(*) as total_employees, 
sum(case when attrition = 'yes' then 1 else 0 END) as employee_left, 
sum(case when attrition = 'yes' then 1 else 0 END)/ Count(*)* 100 as attrition_rate
from employeedata_1
group by department;

2. Average Hourly Rate for Male Research Scientists

SELECT 
AVG(hourly_rate) AS avg_hourly_rate
FROM employeedata_1
WHERE jobrole = 'Research Scientist' AND gender = 'Male';


3. Attrition Rate Vs Monthly Income

SELECT 
CASE 
WHEN monthly_income < 10000 THEN 'Low Income'
WHEN monthly_income >= 10000 AND monthly_income < 30000 THEN 'Medium Income'
ELSE 'High Income' END AS IncomeGroup,
AVG(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) * 100 AS AvgAttritionRatePercentage,
AVG(monthly_income) AS AvgMonthlyIncome
FROM employeedata_1
LEFT JOIN employeedata_2 ON employeedata_1.employee_ID = employeedata_2.employee_ID
GROUP BY IncomeGroup; ORDER BY AvgMonthlyIncome;


4. Job Role Vs Work Life Balance

SELECT
jobrole,
COUNT(*) AS total_employees,
COUNT(CASE WHEN work_life_balance = 1 THEN 1 END) * 100.0 / COUNT(*) AS percentage_rated_one,
COUNT(CASE WHEN work_life_balance = 2 THEN 1 END) * 100.0 / COUNT(*) AS percentage_rated_two,
COUNT(CASE WHEN work_life_balance = 3 THEN 1 END) * 100.0 / COUNT(*) AS percentage_rated_three,
COUNT(CASE WHEN work_life_balance = 4 THEN 1 END) * 100.0 / COUNT(*) AS percentage_rated_four
FROM employeedata_1
GROUP BY jobrole
ORDER BY jobrole;


5. Attrition Rate Vs Year Since Last Promotion

SELECT
CASE 
WHEN years_since_last_promotion > 0 AND years_since_last_promotion <= 10 THEN '1-10'
WHEN years_since_last_promotion > 10 AND years_since_last_promotion <= 20 THEN '10-20'
WHEN years_since_last_promotion > 20 AND years_since_last_promotion <= 30 THEN '20-30'
ELSE '30-40' 
END AS Promotion_band,
AVG(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100 AS Avg_Attrition_Rate
FROM EmployeeData_1
LEFT JOIN employeedata_2 ON EmployeeData_1.employee_ID = employeedata_2.employee_ID
GROUP BY Promotion_band
ORDER BY Promotion_band DESC;









