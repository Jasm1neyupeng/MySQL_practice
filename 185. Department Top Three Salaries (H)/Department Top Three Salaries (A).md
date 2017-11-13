##Answer

雇员表Employee保存了雇员的Id，姓名，薪水，以及部门Id。部门表Department保存了部门的Id和名称。
编写一个SQL查询找出每一个部门薪水排名前3位的雇员信息（排名可以并列），样例如上。

###Idea

首先将雇员表按照雇员的DepartmentId和Salary分别正序和倒序排列；

然后利用MySQL用户定义变量对雇员标记排名rank值，同一部门的rank值从1开始，按照薪水降序递增（注意薪水相同时rank值不变）；

最后筛选rank值不大于3的雇员信息，并与Department表做关联即可。

##SQL

<pre><code>SELECT d.NAME AS Department, t.NAME AS Employee, Salary FROM (
  SELECT    DepartmentId,
            NAME,
            Salary, 
            @rank := IF(@prevDeptId != DepartmentId, 1, 
                         IF(@prevSalary = Salary, @rank, @rank + 1) ) AS Rank,
            @prevDeptId := DepartmentId AS prevDeptId,
            @prevSalary := Salary AS prevSalary
  FROM      Employee e, (SELECT @rank := 0, @prevDeptId := NULL, @prevSalary := NULL) r
  ORDER BY  DepartmentId ASC, Salary DESC
) t INNER JOIN Department d ON t.DepartmentId = d.ID
WHERE t.rank <= 3
</code></pre>

另外，在LeetCode Discuss中看到这样一个短小精悍的解法：

<pre><code>SELECT D.Name AS Department, E.Name AS Employee, E.Salary AS Salary 
FROM Employee E, Department D
WHERE (SELECT COUNT(DISTINCT(Salary)) FROM Employee 
       WHERE DepartmentId = E.DepartmentId AND Salary > E.Salary) < 3
AND E.DepartmentId = D.Id 
ORDER BY E.DepartmentId, E.Salary DESC;
</code></pre>
