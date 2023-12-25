# Tweets' Rolling Averages [Twitter SQL Interview Question]

- Problem level: Medium

- Company: Twitter
- Problem Link: '[here](https://datalemur.com/questions/rolling-average-tweets?referralCode=256wYou1)'

---
<p>This is the same question as problem #10 in the SQL Chapter of  <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Given a table of tweet data over a specified time period, calculate the 3-day rolling average of tweets for each user. Output the user ID, tweet date, and rolling averages rounded to 2 decimal places.</p>
<p>Notes:</p>
<ul>
<li>A rolling average, also known as a moving average or running mean is a time-series technique that examines trends in data over a specified period of time.</li>
<li>In this case, we want to determine how the tweet count for each user changes over a 3-day period.</li>
</ul>
<p><em>Effective April 7th, 2023, the problem statement, solution and hints for this question have been revised.</em></p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">tweet_date</td><td style="text-align:left">timestamp</td></tr><tr><td style="text-align:left">tweet_count</td><td style="text-align:left">integer</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">user_id</th><th style="text-align:left">tweet_date</th><th style="text-align:left">tweet_count</th></tr></thead><tbody><tr><td style="text-align:left">111</td><td style="text-align:left">06/01/2022 00:00:00</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/02/2022 00:00:00</td><td style="text-align:left">1</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/03/2022 00:00:00</td><td style="text-align:left">3</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/04/2022 00:00:00</td><td style="text-align:left">4</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/05/2022 00:00:00</td><td style="text-align:left">5</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">user_id</th><th style="text-align:left">tweet_date</th><th style="text-align:left">rolling_avg_3d</th></tr></thead><tbody><tr><td style="text-align:left">111</td><td style="text-align:left">06/01/2022 00:00:00</td><td style="text-align:left">2.00</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/02/2022 00:00:00</td><td style="text-align:left">1.50</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/03/2022 00:00:00</td><td style="text-align:left">2.00</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/04/2022 00:00:00</td><td style="text-align:left">2.67</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">06/05/2022 00:00:00</td><td style="text-align:left">4.00</td></tr></tbody></table></div>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- A rolling average, also known as a moving average or running mean is a time-series technique that examines trends in data over a specified period of time.
- This is a youtube video about [moving average](https://www.youtube.com/watch?v=Qu-EpmEkS9Q)

---

## Solutions

<details>
<summary> Solution </summary>

You need to know about `ROWS BETWEEN` in SQL
Read [this blog](https://learnsql.com/blog/sql-window-functions-rows-clause/) to understand this topic
You could also read about [window functions](https://learnsql.com/blog/sql-window-functions-cheat-sheet/#window-functions)

```sql
-- website solution
SELECT
    user_id,
    tweet_date,
    ROUND(
        AVG(tweet_count) OVER (
            PARTITION BY user_id
            ORDER BY
                tweet_date ROWS BETWEEN 2 PRECEDING
                AND CURRENT ROW
        ),
        2
    ) AS rolling_avg_3d
FROM
    tweets;

```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
