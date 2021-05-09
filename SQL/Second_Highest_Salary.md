## [第二高的薪水](https://leetcode-cn.com/problems/second-highest-salary/)

排序加选择输出





```sql
SELECT (
    SELECT DISTINCT Salary 
    FROM Employee
    ORDER BY Salary DESC
    LIMIT 1 OFFSET 1
) SecondHighestSalary
```

