##Answer

这道题给了我们一个Weather表，让我们找出比前一天温度高的Id，由于Id的排列未必是按顺序的，所以我们要找前一天就得根据日期来找，我们可以使用MySQL的函数Datadiff来计算两个日期的差值，我们的限制条件是温度高且日期差1，参见代码如下： 

<pre><code>SELECT w1.Id FROM Weather w1, Weather w2
WHERE w1.Temperature > w2.Temperature AND DATEDIFF(w1.Date, w2.Date) = 1;</code></pre>

下面这种解法我们使用了MySQL的TO_DAYS函数，用来将日期换算成天数，其余跟上面相同：

<pre><code>SELECT w1.Id FROM Weather w1, Weather w2
WHERE w1.Temperature > w2.Temperature AND TO_DAYS(w1.Date) = TO_DAYS(w2.Date) + 1;</code></pre>

最后来一种完全不一样的解法，使用了两个变量pre_t和pre_d分别表示上一个温度和上一个日期，然后当前温度要大于上一温度，且日期差为1，满足上述两条件的话选出来为Id，否则为NULL，然后更新pre_t和pre_d为当前的值，最后选出的Id不为空即可：

<pre><code>SELECT Id FROM (
SELECT CASE WHEN Temperature > @pre_t AND DATEDIFF(Date, @pre_d) = 1 THEN Id ELSE NULL END AS Id,
@pre_t := Temperature, @pre_d := Date 
FROM Weather, (SELECT @pre_t := NULL, @pre_d := NULL) AS init ORDER BY Date ASC
) id WHERE Id IS NOT NULL;</code></pre>