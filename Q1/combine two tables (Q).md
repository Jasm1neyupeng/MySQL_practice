##Combine Two Tables
 Table: Person

<pre><code>+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.
</code></pre>

 Table: Address
<pre><code>+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.
</code></pre>
 Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:
 
 ```
 FirstName, LastName, City, State
 ```