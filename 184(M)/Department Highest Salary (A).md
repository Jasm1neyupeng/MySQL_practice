##Answer

雇员表Employee保存了雇员的Id，姓名，薪水以及部门Id。
部门表Department保存了部门的Id和名称。
编写一个SQL查询，找出每一个部门中薪水最高的员工信息。样例及结果如上所示。

###Idea
首先使用临时表t查询出每一个部门的最高薪水，然后使用薪水值和部门Id与雇员表Employee做内连接，再通过部门Id与部门表Department做内连接。

##SQL

<pre><code>SELECT d.Name AS Department, e.Name AS Employee, t.Salary 
FROM Employee e 
INNER JOIN 
(SELECT DepartmentId, MAX(Salary) AS Salary FROM Employee GROUP BY DepartmentId) t
USING(DepartmentId, Salary)
INNER JOIN 
Department d ON d.id = t.DepartmentId</code></pre>