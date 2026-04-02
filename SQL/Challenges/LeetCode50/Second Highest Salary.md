Code:
    
        WITH second_h_Salary as (
        Select
            distinct salary  as SecondHighestSalary 
        From Employee
        order by salary desc
        limit 1 offset 1
        ),
        
        CTE as 
        (
        Select * from second_h_Salary
        UNION 
        Select Null as SecondHighestSalary
        )
        
        Select
            *
        from CTE
        order by SecondHighestSalary desc
        limit 1




Table: Employee

| Column Name | Type |
| :--- | :--- |
| id          | int  |
| salary      | int  |


id is the primary key (column with unique values) for this table.
Each row of this table contains information about the salary of an employee.
 

Write a solution to find the second highest distinct salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).

The result format is in the following example.

**Explanation:**

Example 1:

Input: 
Employee table:


| id | salary |
| :--- | :--- 
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

Output: 


| SecondHighestSalary |
| :--- | 
| 200                 |


Example 2:

Input: 
Employee table:


| id | salary |
| :--- | :--- 
| 1  | 100    |


Output: 

| SecondHighestSalary |
| :--- | 
| null                |
