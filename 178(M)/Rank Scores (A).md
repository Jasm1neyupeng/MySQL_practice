##Answer
编写SQL对分数进行排序。如果两个分数相等，其排名应相同。注意在排名相等的分数之后，下一个排名的数值应该连续。换言之，排名之间不应该有“洞”（跳跃）。
例如给定的分数表，你的查询应该产生的结果如上所示（按照分数递减排序）。

###Idea
使用MySQL的User-Defined Variables（用户定义变量）

##SQL
<pre><code>SELECT Score, Rank FROM(
  SELECT    Score,
            @curRank := @curRank + IF(@prevScore = Score, 0, 1) AS Rank,
            @prevScore := Score
  FROM      Scores s, (SELECT @curRank := 0) r, (SELECT @prevScore := NULL) p
  ORDER BY  Score DESC
) t;</code></pre>