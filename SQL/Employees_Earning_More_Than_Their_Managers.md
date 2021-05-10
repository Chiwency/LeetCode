## [181. 超过经理收入的员工](https://leetcode-cn.com/problems/employees-earning-more-than-their-managers/)

子查询

看题解还有连接的写法，弟弟了





```sql
SELECT  Name Employee
FROM Employee e1
WHERE ManagerId IS NOT NULL AND Salary>(
    SELECT Salary 
    FROM Employee e2
    WHERE e2.Id=e1.ManagerId
)
```

