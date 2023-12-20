# Pharmacy Analytics (Part 3) [CVS Health SQL Interview Question]

- Problem level: Easy

- Company: CVS Health
- Problem Link: '[here](https://datalemur.com/questions/total-drugs-sales?referralCode=256wYou1)'

---
<p>CVS Health wants to gain a clearer understanding of its pharmacy sales and the performance of various products.</p>
<p>Write a query to calculate the total drug sales for each manufacturer. Round the answer to the nearest million and report your results in descending order of total sales. In case of any duplicates, sort them alphabetically by the manufacturer name.</p>
<p>Since this data will be displayed on a dashboard viewed by business stakeholders, please format your results as follows: "$36 million".</p>
<p>If you like this question, try out <a href="https://datalemur.com/questions/top-drugs-sold" rel="noopener noreferrer" target="_blank">Pharmacy Analytics (Part 4)</a>!</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">units_sold</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">total_sales</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">cogs</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">manufacturer</td><td style="text-align:left">varchar</td></tr><tr><td style="text-align:left">drug</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>product_id</strong></th><th style="text-align:left"><strong>units_sold</strong></th><th style="text-align:left"><strong>total_sales</strong></th><th style="text-align:left"><strong>cogs</strong></th><th style="text-align:left"><strong>manufacturer</strong></th><th style="text-align:left"><strong>drug</strong></th></tr></thead><tbody><tr><td style="text-align:left">94</td><td style="text-align:left">132362</td><td style="text-align:left">2041758.41</td><td style="text-align:left">1373721.70</td><td style="text-align:left">Biogen</td><td style="text-align:left">UP and UP</td></tr><tr><td style="text-align:left">9</td><td style="text-align:left">37410</td><td style="text-align:left">293452.54</td><td style="text-align:left">208876.01</td><td style="text-align:left">Eli Lilly</td><td style="text-align:left">Zyprexa</td></tr><tr><td style="text-align:left">50</td><td style="text-align:left">90484</td><td style="text-align:left">2521023.73</td><td style="text-align:left">2742445.9</td><td style="text-align:left">Eli Lilly</td><td style="text-align:left">Dermasorb</td></tr><tr><td style="text-align:left">61</td><td style="text-align:left">77023</td><td style="text-align:left">500101.61</td><td style="text-align:left">419174.97</td><td style="text-align:left">Biogen</td><td style="text-align:left">Varicose Relief</td></tr><tr><td style="text-align:left">136</td><td style="text-align:left">144814</td><td style="text-align:left">1084258.00</td><td style="text-align:left">1006447.73</td><td style="text-align:left">Biogen</td><td style="text-align:left">Burkhart</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>manufacturer</strong></th><th style="text-align:left"><strong>sale</strong></th></tr></thead><tbody><tr><td style="text-align:left">Biogen</td><td style="text-align:left">$4 million</td></tr><tr><td style="text-align:left">Eli Lilly</td><td style="text-align:left">$3 million</td></tr></tbody></table></div>
<h3>Explanation</h3>
<p>The total sales for Biogen is $4 million ($2,041,758.41 + $500,101.61 + $1,084,258.00 = $3,626,118.02) and for Eli Lilly is $3 million ($293,452.54 + $2,521,023.73 = $2,814,476.27).</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- `ROUND` the nearest million we could use `ROUND( number / 1000000.0)`
- In formating you could concatenating them by `||` or `CONCAT()` function

---

## Solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    manufacturer,
    '$' || ROUND(SUM(total_sales) / 1000000.0) || ' million' as sale
FROM
    pharmacy_sales
GROUP BY
    manufacturer
ORDER BY
    SUM(total_sales) DESC,
    manufacturer
```

</details>
---

<details>
<summary> Solution 2</summary>

using CTE

```sql
WITH drug_sales AS (
    SELECT
        manufacturer,
        SUM(total_sales) as sales
    FROM
        pharmacy_sales
    GROUP BY
        manufacturer
)
SELECT
    manufacturer,
    ('$' || ROUND(sales / 1000000) || ' million') AS sales_mil
FROM
    drug_sales
ORDER BY
    sales DESC,
    manufacturer;
```

</details>

<details>
<summary> Solution 3</summary>

Using sub-query

```sql
SELECT
    manufacturer,
    '$' || sale_by_m || ' million' as sales
from
    (
        SELECT
            manufacturer,
            ROUND(SUM(total_sales) / 1000000.0) sale_by_m
        FROM
            pharmacy_sales
        GROUP BY
            manufacturer
        ORDER BY
            SUM(total_sales) DESC,
            manufacturer ASC
    ) sub
```

</details>
---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
