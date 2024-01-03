# Histogram of Users and Purchases [Walmart SQL Interview Question]

- Problem level: Medium

- Company: Walmart
- Problem Link: '[here](https://datalemur.com/questions/histogram-users-purchases?referralCode=256wYou1)'

---
<p>This is the same question as problem #13 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you're given a table on Walmart user transactions. Based on their most recent transaction date, write a query that retrieve the users along with the number of products they bought.</p>
<p>Output the user's most recent transaction date, user ID, and the number of products, sorted in chronological order by the transaction date.</p>
<p><em>Starting from November 10th, 2022, the official solution was updated, and the expected output of transaction date, number of users, and number of products was changed to the current expected output.</em></p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">spend</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">transaction_date</td><td style="text-align:left">timestamp</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">product_id</th><th style="text-align:left">user_id</th><th style="text-align:left">spend</th><th style="text-align:left">transaction_date</th></tr></thead><tbody><tr><td style="text-align:left">3673</td><td style="text-align:left">123</td><td style="text-align:left">68.90</td><td style="text-align:left">07/08/2022 12:00:00</td></tr><tr><td style="text-align:left">9623</td><td style="text-align:left">123</td><td style="text-align:left">274.10</td><td style="text-align:left">07/08/2022 12:00:00</td></tr><tr><td style="text-align:left">1467</td><td style="text-align:left">115</td><td style="text-align:left">19.90</td><td style="text-align:left">07/08/2022 12:00:00</td></tr><tr><td style="text-align:left">2513</td><td style="text-align:left">159</td><td style="text-align:left">25.00</td><td style="text-align:left">07/08/2022 12:00:00</td></tr><tr><td style="text-align:left">1452</td><td style="text-align:left">159</td><td style="text-align:left">74.50</td><td style="text-align:left">07/10/2022 12:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">transaction_date</th><th style="text-align:left">user_id</th><th style="text-align:left">purchase_count</th></tr></thead><tbody><tr><td style="text-align:left">07/08/2022 12:00:00</td><td style="text-align:left">115</td><td style="text-align:left">1</td></tr><tr><td style="text-align:left">07/08/2022 12:00:000</td><td style="text-align:left">123</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">07/10/2022 12:00:00</td><td style="text-align:left">159</td><td style="text-align:left">1</td></tr></tbody></table></div>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

---

## Solutions

<details>
<summary> Solution </summary>

```sql
with user_and_min_time as (
    SELECT
        MAX(transaction_date) min_transaction_date,
        user_id
    FROM
        user_transactions
    GROUP BY
        user_id
)
SELECT
    u.transaction_date,
    u.user_id,
    count(1) purchase_count
FROM
    user_transactions AS u
    INNER JOIN user_and_min_time AS m ON u.user_id = m.user_id
    and u.transaction_date = m.min_transaction_date
GROUP BY
    (u.transaction_date, u.user_id)
ORDER BY
    u.transaction_date

```

</details>

<details>
<summary> Solution </summary>
website solution

```sql

WITH latest_transactions_cte AS (
    SELECT
        transaction_date,
        user_id,
        product_id,
        RANK() OVER (
            PARTITION BY user_id
            ORDER BY
                transaction_date DESC
        ) AS transaction_rank
    FROM
        user_transactions
)
SELECT
    transaction_date,
    user_id,
    COUNT(product_id) AS purchase_count
FROM
    latest_transactions_cte
WHERE
    transaction_rank = 1
GROUP BY
    transaction_date,
    user_id
ORDER BY
    transaction_date;

```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
