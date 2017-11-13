##Answer
编写一个SQL查询获取雇员表中的第二高的薪水值。
例如，上表中的第二高薪水为200.如果没有第二高薪水，查询应该返回null

###Idea
题目中所谓的“第二高”是指去重后的仅次于最高值的分数。
因此只需借助于MAX关键词即可完成题目。

##SQL

<pre><code>SELECT MAX(Salary) FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee);
</code></pre>

等同于
<pre><code>SELECT MAX(Salary) FROM Employee 
WHERE Salary NOT IN
(SELECT MAX(Salary) FROM Employee);
</code></pre>

如果不去重

<pre><code>SELECT (SELECT Salary AS SecondHighestSalary 
FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 1);
</code></pre>