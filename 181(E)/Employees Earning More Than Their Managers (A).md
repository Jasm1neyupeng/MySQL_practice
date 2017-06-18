##Answer
雇员表记录了所有雇员的信息，包括他们的经理在内。每一个雇员都有一个Id，和他的经理的Id。
给定雇员表，编写一个SQL查询找出薪水大于经理的员工姓名。对于上表来说，Joe是唯一收入大于经理的员工。

###Idea
自连接

##SQL
<pre><code>SELECT a.NAME FROM Employee a, Employee b 
WHERE a.ManagerId = b.Id AND a.Salary > b.Salary;
</code></pre>