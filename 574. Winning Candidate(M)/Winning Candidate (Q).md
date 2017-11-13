##574. Winning Candidate
Table: Candidate
<pre><code>+-----+---------+
| id  | Name    |
+-----+---------+
| 1   | A       |
| 2   | B       |
| 3   | C       |
| 4   | D       |
| 5   | E       |
+-----+---------+  </code></pre>
Table: Vote
<pre><code>+-----+--------------+
| id  | CandidateId  |
+-----+--------------+
| 1   |     2        |
| 2   |     4        |
| 3   |     3        |
| 4   |     2        |
| 5   |     5        |
+-----+--------------+</code></pre>
id is the auto-increment primary key,
CandidateId is the id appeared in Candidate table.

Write a sql to find the name of the winning candidate, the above example will return the winner B.

<pre><code>+------+
| Name |
+------+
| B    |
+------+</code></pre>

Notes:
You may assume there is no tie, in other words there will be at most one winning candidate.