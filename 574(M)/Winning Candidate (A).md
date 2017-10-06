##Approach: 
Using JOIN and a temporary table 

###Algorithm

Query in the Vote table to get the winner's id and then join it with the Candidate table to get the name.

<pre><code>SELECT
    name AS 'Name'
FROM
    Candidate
        JOIN
    (SELECT
        Candidateid
    FROM
        Vote
    GROUP BY Candidateid
    ORDER BY COUNT(*) DESC
    LIMIT 1) AS winner
WHERE
    Candidate.id = winner.Candidateid;</code></pre>
