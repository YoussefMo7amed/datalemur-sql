# Histogram of Tweets [Twitter SQL Interview Question]

- Problem level: Easy

- Company: Twitter
- Problem Link: '[here](https://datalemur.com/questions/sql-histogram-tweets)'

---
<p>This is the same question as problem #6 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you're given a table Twitter tweet data, write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket.</p>
<p>In other words, group the users by the number of tweets they posted in 2022 and count the number of users in each group.</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">tweet_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">msg</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">tweet_date</td><td style="text-align:left">timestamp</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">tweet_id</th><th style="text-align:left">user_id</th><th style="text-align:left">msg</th><th style="text-align:left">tweet_date</th></tr></thead><tbody><tr><td style="text-align:left">214252</td><td style="text-align:left">111</td><td style="text-align:left">Am considering taking Tesla private at $420. Funding secured.</td><td style="text-align:left">12/30/2021 00:00:00</td></tr><tr><td style="text-align:left">739252</td><td style="text-align:left">111</td><td style="text-align:left">Despite the constant negative press covfefe</td><td style="text-align:left">01/01/2022 00:00:00</td></tr><tr><td style="text-align:left">846402</td><td style="text-align:left">111</td><td style="text-align:left">Following @NickSinghTech on Twitter changed my life!</td><td style="text-align:left">02/14/2022 00:00:00</td></tr><tr><td style="text-align:left">241425</td><td style="text-align:left">254</td><td style="text-align:left">If the salary is so competitive why won’t you tell me what it is?</td><td style="text-align:left">03/01/2022 00:00:00</td></tr><tr><td style="text-align:left">231574</td><td style="text-align:left">148</td><td style="text-align:left">I no longer have a manager. I can't be managed</td><td style="text-align:left">03/23/2022 00:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">tweet_bucket</th><th style="text-align:left">users_num</th></tr></thead><tbody><tr><td style="text-align:left">1</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">2</td><td style="text-align:left">1</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Based on the example output, there are two users who posted only one tweet in 2022, and one user who posted two tweets in 2022. The query groups the users by the number of tweets they posted and displays the number of users in each group.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- You can david the problem into sub-problems
  - number of tweets for each user (group)
  - filter by date
- After knowing number of tweets for each user, can i know the occurrence of each number

---

## Solutions

<details>
<summary> Solution 1</summary>

```sql
select
    per_user as tweet_bucket,
    count(per_user)
from
    (
        select
            count(1) per_user
        from
            tweets
        where
            tweet_date BETWEEN '2022-01-01'
            and '2022-12-31'
        group by
            user_id
    ) sub
GROUP BY
    per_user
```

</details>
<details>
<summary> Solution 2</summary>

Using [CTE](https://datalemur.com/sql-tutorial/sql-cte-subquery)

```sql
WITH total_tweets AS (
    SELECT
        user_id,
        COUNT(tweet_id) AS tweet_count_per_user
    FROM
        tweets
    WHERE
        tweet_date BETWEEN '2022-01-01'
        AND '2022-12-31'
    GROUP BY
        user_id
)

SELECT
    tweet_count_per_user AS tweet_bucket,
    COUNT(user_id) AS users_num
FROM
    total_tweets
GROUP BY
    tweet_count_per_user;
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
