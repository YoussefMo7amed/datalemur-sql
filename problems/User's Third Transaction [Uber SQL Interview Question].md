# User's Third Transaction [Uber SQL Interview Question]

- Problem level: Medium

- Company: Uber
- Problem Link: '[here](https://datalemur.com/questions/sql-third-transaction?referralCode=256wYou1)'

---
<p>This is the same question as problem #11 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you are given the table below on Uber transactions made by users. Write a query to obtain the third transaction of every user. Output the user id, spend and transaction date.</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">spend</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">transaction_date</td><td style="text-align:left">timestamp</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>user_id</strong></th><th style="text-align:left"><strong>spend</strong></th><th style="text-align:left"><strong>transaction_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">111</td><td style="text-align:left">100.50</td><td style="text-align:left">01/08/2022 12:00:00</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">55.00</td><td style="text-align:left">01/10/2022 12:00:00</td></tr><tr><td style="text-align:left">121</td><td style="text-align:left">36.00</td><td style="text-align:left">01/18/2022 12:00:00</td></tr><tr><td style="text-align:left">145</td><td style="text-align:left">24.99</td><td style="text-align:left">01/26/2022 12:00:00</td></tr><tr><td style="text-align:left">111</td><td style="text-align:left">89.60</td><td style="text-align:left">02/05/2022 12:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>user_id</strong></th><th style="text-align:left"><strong>spend</strong></th><th style="text-align:left"><strong>transaction_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">111</td><td style="text-align:left">89.60</td><td style="text-align:left">02/05/2022 12:00:00</td></tr></tbody></table></div>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

---

## Solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    user_id,
    spend,
    transaction_date
FROM
    (
        SELECT
            user_id,
            spend,
            transaction_date,
            row_number() OVER (
                PARTITION BY user_id
                order by
                    transaction_date
            ) no
        from
            transactions
    ) sub
where
    no = 3

```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
