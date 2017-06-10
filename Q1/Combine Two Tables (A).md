##Answer
编写一个SQL查询，对于Person表中的每一个人，取出FirstName, LastName, City, State属性，无论其地址信息是否存在。

###Idea
Person表是主表，Address表是从表，通过Left Outer Join左外连接即可。

##SQL
<pre><code>SELECT p.FirstName, p.LastName, a.City, a.State
FROM Person p LEFT OUTER JOIN Address a USING (PersonId);
</code></pre>