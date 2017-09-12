##题目大意：
Trips表存储出租车旅程记录。每一个旅程包含一个唯一的Id，Client_Id与Driver_Id都是Users表中Users_Id的外键。Status是枚举类型 (‘completed’, ‘cancelled by driver’, ‘cancelled by client’)。

Users表存储用户信息。每一个用户都包含一个唯一的Users_Id以及角色Role，枚举类型(‘client’, ‘driver’, ‘partner’)。

编写SQL查询统计日期范围2013-10-01到2013-10-03之间的旅程取消率。对于上面的两张表，你的SQL查询应当返回下面的结果，取消率应四舍五入保留2位小数。

###解题思路
利用IF函数与SUM函数组合查询

###Answer
<pre><code>SELECT t.Request_at AS `Day`, 
ROUND(SUM(IF(t.Status = 'completed', 0, 1)) / COUNT(*), 2) AS `Cancellation Rate` 
FROM Trips t INNER JOIN Users u ON t.Client_Id = u.Users_Id 
WHERE t.Request_at BETWEEN '2013-10-01' AND '2013-10-03' 
AND u.Banned = 'No' AND u.Role = 'client' 
GROUP BY t.Request_at ORDER BY t.Request_at;
</code></pre>
