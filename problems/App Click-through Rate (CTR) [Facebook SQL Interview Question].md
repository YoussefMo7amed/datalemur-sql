# App Click-through Rate (CTR) [Facebook SQL Interview Question]

- Problem level: Easy

- Company: Facebook
- Problem Link: '[here](https://datalemur.com/questions/click-through-rate?referralCode=256wYou1)'

---
<p>This is the same question as problem #1 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you have an events table on Facebook app analytics. Write a query to calculate the click-through rate (CTR) for the app in 2022 and round the results to 2 decimal places.</p>
<p>Definition and note:</p>
<ul>
<li>Percentage of click-through rate (CTR) = 100.0 * Number of clicks / Number of impressions</li>
<li>To avoid integer division, multiply the CTR by 100.0, not 100.</li>
</ul>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">app_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">event_type</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">timestamp</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">app_id</th><th style="text-align:left">event_type</th><th style="text-align:left">timestamp</th></tr></thead><tbody><tr><td style="text-align:left">123</td><td style="text-align:left">impression</td><td style="text-align:left">07/18/2022 11:36:12</td></tr><tr><td style="text-align:left">123</td><td style="text-align:left">impression</td><td style="text-align:left">07/18/2022 11:37:12</td></tr><tr><td style="text-align:left">123</td><td style="text-align:left">click</td><td style="text-align:left">07/18/2022 11:37:42</td></tr><tr><td style="text-align:left">234</td><td style="text-align:left">impression</td><td style="text-align:left">07/18/2022 14:15:12</td></tr><tr><td style="text-align:left">234</td><td style="text-align:left">click</td><td style="text-align:left">07/18/2022 14:16:12</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">app_id</th><th style="text-align:left">ctr</th></tr></thead><tbody><tr><td style="text-align:left">123</td><td style="text-align:left">50.00</td></tr><tr><td style="text-align:left">234</td><td style="text-align:left">100.00</td></tr></tbody></table></div>
<h3>Explanation</h3>
<p>Let's consider an example of App 123. This app has a click-through rate (CTR) of 50.00% because out of the 2 impressions it received, it got 1 click.</p>
<p>To calculate the CTR, we divide the number of clicks by the number of impressions, and then multiply the result by 100.0 to express it as a percentage. In this case, 1 divided by 2 equals 0.5, and when multiplied by 100.0, it becomes 50.00%. So, the CTR of App 123 is 50.00%.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- sometime you need to get focus first on the condition that you want to put in `where`

---

## Solutions

<details>
<summary> Solution </summary>

Here i used

- [`CASE`](https://www.w3schools.com/sql/sql_case.asp)
  - You can use [`filter`](https://modern-sql.com/feature/filter)
- [`EXTRACT`](https://www.w3schools.com/sql/func_mysql_extract.asp)
  - You can also use [`between`](https://www.w3schools.com/sql/sql_between.asp)

```sql
SELECT
    app_id,
    ROUND(
        sum(
            CASE
                WHEN event_type = 'click' THEN 1
                ELSE 0
            END
        ) * 100.0 / SUM(
            CASE
                WHEN event_type = 'impression' THEN 1
                ELSE 0
            END
        ),
        2
    ) ctr
FROM
    events
WHERE
    EXTRACT(
        Year
        from
            timestamp
    ) = 2022
GROUP BY
    app_id
```

</details>

website solutions
<details>
<summary> Solution </summary>

```sql
SELECT
    app_id,
    ROUND(
        100.0 * COUNT(
            CASE
                WHEN event_type = 'click' THEN 1
                ELSE NULL
            END
        ) / COUNT(
            CASE
                WHEN event_type = 'impression' THEN 1
                ELSE NULL
            END
        ),
        2
    ) AS ctr_rate
FROM
    events
WHERE
    timestamp >= '2022-01-01'
    AND timestamp < '2023-01-01'
GROUP BY
    app_id;
```

</details>
<details>
<summary> Solution </summary>

```sql
SELECT
    app_id,
    ROUND(
        100.0 * SUM(1) FILTER (
            WHERE
                event_type = 'click'
        ) / SUM(1) FILTER (
            WHERE
                event_type = 'impression'
        ),
        2
    ) AS ctr_app
FROM
    events
WHERE
    timestamp >= '2022-01-01'
    AND timestamp < '2023-01-01'
GROUP BY
    app_id;
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
