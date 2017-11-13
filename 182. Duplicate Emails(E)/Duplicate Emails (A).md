##Answer

编写SQL删除Person表中所有的重复email条目，只保留Id最小的唯一email记录。其中，Id是表的主键。

##SQL
<pre><code>DELETE p1 FROM Person p1 INNER JOIN Person p2
WHERE p1.Email = p2.Email AND p1.Id > p2.Id;
</code></pre>


<pre><code>DELETE FROM p1 USING Person p1 INNER JOIN Person p2
WHERE p1.Email = p2.Email AND p1.Id > p2.Id;
</code></pre>


<pre><code>DELETE FROM Person WHERE ID NOT IN 
(SELECT * FROM (SELECT MIN(Id) FROM Person p GROUP BY Email) t);
</code></pre>