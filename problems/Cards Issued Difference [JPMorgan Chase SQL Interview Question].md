# Cards Issued Difference [JPMorgan Chase SQL Interview Question]

- Problem level: Easy

- Company: JPMorgan Chase
- Problem Link: '[here](https://datalemur.com/questions/cards-issued-difference?referralCode=256wYou1)'

---
<p>Your team at JPMorgan Chase is preparing to launch a new credit card, and to gain some insights, you're analyzing how many credit cards were issued each month.</p>
<p>Write a query that outputs the name of each credit card and the difference in the number of issued cards between the month with the highest issuance cards and the lowest issuance. Arrange the results based on the largest disparity.</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">issue_month</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">issue_year</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">card_name</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">issued_amount</td><td style="text-align:left">integer</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">card_name</th><th style="text-align:left">issued_amount</th><th style="text-align:left">issue_month</th><th style="text-align:left">issue_year</th></tr></thead><tbody><tr><td style="text-align:left">Chase Freedom Flex</td><td style="text-align:left">55000</td><td style="text-align:left">1</td><td style="text-align:left">2021</td></tr><tr><td style="text-align:left">Chase Freedom Flex</td><td style="text-align:left">60000</td><td style="text-align:left">2</td><td style="text-align:left">2021</td></tr><tr><td style="text-align:left">Chase Freedom Flex</td><td style="text-align:left">65000</td><td style="text-align:left">3</td><td style="text-align:left">2021</td></tr><tr><td style="text-align:left">Chase Freedom Flex</td><td style="text-align:left">70000</td><td style="text-align:left">4</td><td style="text-align:left">2021</td></tr><tr><td style="text-align:left">Chase Sapphire Reserve</td><td style="text-align:left">170000</td><td style="text-align:left">1</td><td style="text-align:left">2021</td></tr><tr><td style="text-align:left">Chase Sapphire Reserve</td><td style="text-align:left">175000</td><td style="text-align:left">2</td><td style="text-align:left">2021</td></tr><tr><td style="text-align:left">Chase Sapphire Reserve</td><td style="text-align:left">180000</td><td style="text-align:left">3</td><td style="text-align:left">2021</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">card_name</th><th style="text-align:left">difference</th></tr></thead><tbody><tr><td style="text-align:left">Chase Freedom Flex</td><td style="text-align:left">15000</td></tr><tr><td style="text-align:left">Chase Sapphire Reserve</td><td style="text-align:left">10000</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Chase Freedom Flex's best month was 70k cards issued and the worst month was 55k cards, so the difference is 15k cards.</p>
<p>Chase Sapphire Reserve’s best month was 180k cards issued and the worst month was 170k cards, so the difference is 10k cards.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

It's very straightforward you got the max value - min value but there is a question
*Does they cares about the year?*

---

## Solutions

<details>
<summary> Solution </summary>

Note here we neglected the year (but it accepted answer)

```sql
SELECT
    card_name,
    MAX(issued_amount) - MIN(issued_amount) AS difference
from
    monthly_cards_issued
GROUP BY
    card_name
ORDER BY
    difference DESC
```

if we do care about the year also (difference between each month within the same year)

```sql
SELECT
    card_name,
    MAX(issued_amount) - MIN(issued_amount) AS difference
from
    monthly_cards_issued
GROUP BY
    (card_name, issue_year)
ORDER BY
    difference DESC
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
