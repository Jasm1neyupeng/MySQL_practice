##题目大意：
给定数据表Numbers，包含两列（数字Number及其频率Frequency）

编写查询计算Number的中位数median。

###解题思路：
使用MySQL的User-Defined Variables（用户定义变量）。

构造中间表t，包含列Number, Frequency, AccFreq（累积频率）, SumFreq（频率求和）

例如样例数据得到的中间表结果为
<pre><code>+----------+-------------+-----------+----------+
|  Number  |  Frequency  |  AccFreq  | SumFreq  |
+----------+-------------|-----------|----------|
|  0       |  7          |  7        |  12      |
|  1       |  1          |  8        |  12      |
|  2       |  3          |  11       |  12      |
|  3       |  1          |  12       |  12      |
+----------+-------------+-----------+----------+</code></pre>
AccFreq范围在[SumFreq / 2, SumFreq / 2 + Frequency]的Number均值即为答案。

AccFreq范围的推导过程如下：

<pre><code>AccFreq BETWEEN SumFreq / 2 AND SumFreq / 2 + 1 OR AccFreq - Frequency <= SumFreq / 2 AND AccFreq > SumFreq / 2 + 1</code></pre>
上式含义为：

<pre><code>AccFreq本身介于[SumFreq / 2, SumFreq / 2 + 1]之间
或者上一行的AccFreq <= SumFreq / 2 并且 当前行的AccFreq > SumFreq / 2 + 1</code></pre>

两种情况合并即可得到AccFreq的范围：

<pre><code>AccFreq BETWEEN SumFreq / 2 AND SumFreq / 2 + Frequency</code></pre>
###SQL语句：
<pre><code> #Write your MySQL query statement below
SELECT AVG(Number) AS median FROM (
  SELECT Number, Frequency, AccFreq, SumFreq FROM
  (SELECT    Number,
             Frequency, @curFreq := @curFreq + Frequency AS AccFreq
   FROM      Numbers n, (SELECT @curFreq := 0) r
   ORDER BY  Number) t1,
  (SELECT SUM(Frequency) SumFreq FROM Numbers) t2
) t
WHERE AccFreq BETWEEN SumFreq / 2 AND SumFreq / 2 + Frequency</code></pre>

