# SQL #001
## Histogram of Tweets
Site: [[DataLemur](https://datalemur.com/)]\
Difficulty per Site: Easy

Problem
Assume you're given a table Twitter tweet data, write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket. In other words, group the users by the number of tweets they posted in 2022 and count the number of users in each group. [[Full Description](https://datalemur.com/questions/sql-histogram-tweets)]

## ✅ Submitted Solution
This solution is functionally correct and achieves the goal of counting users per tweet bucket. However, it uses DISTINCT unnecessarily in the outer query, which adds overhead without benefit since the GROUP BY already ensures uniqueness.

``` SELECT 
  DISTINCT tweet_bucket, COUNT(users_id) AS users_num FROM (
      SELECT COUNT(DISTINCT tweet_id) AS tweet_bucket, user_id AS users_id
      FROM tweets
      WHERE EXTRACT (YEAR FROM tweet_date) = 2022
      GROUP BY user_id) as users_tweets
GROUP BY tweet_bucket;
```
## 🚀 Advanced Solution
Uses a Common Table Expression (CTE) and avoids unnecessary DISTINCT 
```
WITH cte AS (
  SELECT
    user_id
    ,COUNT(tweet_id) AS count
  FROM tweets
  WHERE EXTRACT(YEAR FROM tweet_date) = 2022
  GROUP BY user_id
)
SELECT
  count AS tweet_buket, COUNT(user_id) AS users_num
FROM cte 
GROUP BY count;
```
