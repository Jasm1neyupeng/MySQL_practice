##Customers Who Never Order

Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.

Table: Customers.

<pre><code>+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+</code></pre>

Table: Orders
<pre><code>+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+</code></pre>

Using the above tables as example, return the following:
<pre><code>+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+</code></pre>