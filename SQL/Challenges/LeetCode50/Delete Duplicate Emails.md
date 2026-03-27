Delete Duplicate Emails:

There are several solutions to this problem, One I used was using the row_number which was not optimized

    With Duplicate_Emails as (
    Select
      id,
      email,
      row_number() over (partition by email order by id )  as E_mail_rank
    
    From Person
    )
    DELETE p FROM Person p
    JOIN Duplicate_Emails d on d.id = p.id 
    WHERE E_mail_rank > 1


Another way to approach this problem is refactoring duplicate email deletion to use a self-join. 
This approach is significantly more performant, as relational databases are highly optimized for executing joins and utilizing indexes

    DELETE p1 FROM Person p1
    join Person p2 on p1.email = p2.email 
        and p1.id > p2.id


Problem :

| Column Name | Type    |
| :--- | :--- |
| id          | int     |
| email       | varchar |


id is the primary key (column with unique values) for this table.
Each row of this table contains an email. The emails will not contain uppercase letters.
 

Write a solution to delete all duplicate emails, keeping only one unique email with the smallest id.

For SQL users, please note that you are supposed to write a DELETE statement and not a SELECT one.

For Pandas users, please note that you are supposed to modify Person in place.

After running your script, the answer shown is the Person table. The driver will first compile and run your piece of code and then show the Person table. The final order of the Person table does not matter.

The result format is in the following example.


Input: 
Person table:
| id | email            |
| :--- | :--- |
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |


Output: 

| id | email            |
| :--- | :--- |
| 1  | john@example.com |
| 2  | bob@example.com  |


Explanation: john@example.com is repeated two times. We keep the row with the smallest Id = 1.
