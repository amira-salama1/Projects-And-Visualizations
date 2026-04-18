
Friend Requests II: Who Has the Most Friends

So, the idea is simple if you think that you need to get a table/result with the user ID and count of friends

SQL Code:

          # Write your MySQL query statement below
          with Req as (
          select
             requester_id ,
             count(*) as req_count
          from RequestAccepted
          group by requester_id
          ) ,
          Accepted  as (
          select
             accepter_id  ,
             count(*) as acc_count
          from RequestAccepted
          group by accepter_id
          
          ) , 
          CTE as (
          select 
              requester_id as id ,
              req_count as num 
          from Req
          
          UNION ALL
          
          Select 
              accepter_id as id,  
              acc_count as num
          from Accepted
          )
          
          Select
              id,
              sum(num) as num 
          From CTE 
          group by id
          order by num desc
          limit 1

**Problem Description:**
 
| Column Name    | Type    |
--:|--:|
| requester_id   | int     |
| accepter_id    | int     |
| accept_date    | date    |

* (requester_id, accepter_id) is the primary key (combination of columns with unique values) for this table.
* This table contains the ID of the user who sent the request, the ID of the user who received the request, and the date when the request was accepted.
* Write a solution to find the people who have the most friends and the most friends number.
* The test cases are generated so that only one person has the most friends.
* The result format is in the following example.

  Example 1:

Input: 
RequestAccepted table:

| requester_id | accepter_id | accept_date |
--:|--:|--:|
| 1            | 2           | 2016/06/03  |
| 1            | 3           | 2016/06/08  |
| 2            | 3           | 2016/06/08  |
| 3            | 4           | 2016/06/09  |

Output: 

| id | num |
--:|--:|
| 3  | 3   |

Explanation: 
* The person with id 3 is a friend of people 1, 2, and 4, so he has three friends in total, which is the most number than any others.
