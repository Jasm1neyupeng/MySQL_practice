###Answer
选出所有奖金<1000元的雇员姓名及奖金数额

<pre><code>SELECT name, bonus 
FROM Employee LEFT JOIN Bonus USING (empId)
WHERE IFNULL(bonus, 0) < 1000</code></pre>
