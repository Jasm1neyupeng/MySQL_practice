##Answer

编写SQL查询获取雇员表中的第n高薪水值。
例如，给定上面的雇员表，当n为2时，第n高薪水为200.如果没有第n高薪水，查询返回null。

###Idea
Limit 和 order by

##SQL

	CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
	BEGIN
	DECLARE M INT;
	SET M=N-1;
  	RETURN (
    	  # Write your MySQL query statement below.
      	SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT M, 1
 	 );
	END
