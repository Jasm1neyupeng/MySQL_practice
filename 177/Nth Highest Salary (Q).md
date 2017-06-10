##Nth Highest Salary
Write a SQL query to get the nth highest salary from the Employee table.

<pre><code>+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
</code></pre>

For example, given the above Employee table, the nth highest salary where n = 2 is 200. If there is no nth highest salary, then the query should return null.

<pre><code>+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+</code></pre>
