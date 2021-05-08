## [175. 组合两个表](https://leetcode-cn.com/problems/combine-two-tables/)

外连接



```sql
SELECT Person.FirstName,Person.LastName,Address.City,Address.State
FROM Person
LEFT JOIN Address
On Person.PersonId=Address.PersonId
```





