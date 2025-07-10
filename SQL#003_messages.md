# SQL #003
## Power Users
Site: [[DataLemur](https://datalemur.com/)]\
Difficulty per Site: Medium

## Problem
Write a query to identify the top 2 Power Users who sent the highest number of messages on Microsoft Teams in August 2022. Display the IDs of these 2 users along with the total number of messages they sent. [[Full Description]([https://datalemur.com/questions/sql-histogram-tweets](https://datalemur.com/questions/teams-power-users))]

## ✅ Submitted Solution
This solution is functionally correct and achieves the goal of counting users per message. 

```
SELECT sender_id, COUNT(message_id) AS message_count
FROM messages
WHERE EXTRACT(YEAR FROM sent_date) = 2022 AND 
EXTRACT(MONTH FROM sent_date) = 08
GROUP BY sender_id
ORDER BY COUNT(message_id) DESC
LIMIT 2;
```
## 🚀 Advanced Solution
Not necessirly more advanced but the operation appears more elegant. 
```
SELECT sender_id, COUNT(message_id) AS message_count
FROM messages
WHERE sent_date BETWEEN '2022-08-01' AND '2022-08-31'
GROUP BY sender_id
ORDER BY message_count DESC
LIMIT 2;

```
