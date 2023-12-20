# Pharmacy Analytics (Part 2) [CVS Health SQL Interview Question]

- Problem level: Easy

- Company: CVS Health
- Problem Link: '[here](https://datalemur.com/questions/non-profitable-drugs?referralCode=256wYou1)'

---
<p>CVS Health is analyzing its pharmacy sales data, and how well different products are selling in the market. Each drug is exclusively manufactured by a single manufacturer.</p>
<p>Write a query to identify the manufacturers associated with the drugs that resulted in losses for CVS Health and calculate the total amount of losses incurred.</p>
<p>Output the manufacturer's name, the number of drugs associated with losses, and the total losses in absolute value. Display the results sorted in descending order with the highest losses displayed at the top.</p>
<p>If you like this question, try out <a href="https://datalemur.com/questions/total-drugs-sales" rel="noopener noreferrer" target="_blank">Pharmacy Analytics (Part 3)</a>!</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">units_sold</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">total_sales</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">cogs</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">manufacturer</td><td style="text-align:left">varchar</td></tr><tr><td style="text-align:left">drug</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>product_id</strong></th><th style="text-align:left"><strong>units_sold</strong></th><th style="text-align:left"><strong>total_sales</strong></th><th style="text-align:left"><strong>cogs</strong></th><th style="text-align:left"><strong>manufacturer</strong></th><th style="text-align:left"><strong>drug</strong></th></tr></thead><tbody><tr><td style="text-align:left">156</td><td style="text-align:left">89514</td><td style="text-align:left">3130097.00</td><td style="text-align:left">3427421.73</td><td style="text-align:left">Biogen</td><td style="text-align:left">Acyclovir</td></tr><tr><td style="text-align:left">25</td><td style="text-align:left">222331</td><td style="text-align:left">2753546.00</td><td style="text-align:left">2974975.36</td><td style="text-align:left">AbbVie</td><td style="text-align:left">Lamivudine and Zidovudine</td></tr><tr><td style="text-align:left">50</td><td style="text-align:left">90484</td><td style="text-align:left">2521023.73</td><td style="text-align:left">2742445.90</td><td style="text-align:left">Eli Lilly</td><td style="text-align:left">Dermasorb TA Complete Kit</td></tr><tr><td style="text-align:left">98</td><td style="text-align:left">110746</td><td style="text-align:left">813188.82</td><td style="text-align:left">140422.87</td><td style="text-align:left">Biogen</td><td style="text-align:left">Medi-Chord</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>manufacturer</strong></th><th style="text-align:left"><strong>drug_count</strong></th><th style="text-align:left"><strong>total_loss</strong></th></tr></thead><tbody><tr><td style="text-align:left">Biogen</td><td style="text-align:left">1</td><td style="text-align:left">297324.73</td></tr><tr><td style="text-align:left">AbbVie</td><td style="text-align:left">1</td><td style="text-align:left">221429.36</td></tr><tr><td style="text-align:left">Eli Lilly</td><td style="text-align:left">1</td><td style="text-align:left">221422.17</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>The first three rows indicate that some drugs resulted in losses. Among these, Biogen had the highest losses, followed by AbbVie and Eli Lilly. However, the Medi-Chord drug manufactured by Biogen reported a profit and was excluded from the result.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

---

## Solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    manufacturer,
    COUNT(1) drug_count,
    - SUM(total_sales - cogs) total_loss
FROM
    pharmacy_sales
WHERE
    total_sales - cogs < 0
GROUP BY
    manufacturer
ORDER BY
    total_loss DESC
```

You can also use `abs()` function

```sql
SELECT
    manufacturer,
    COUNT(1) drug_count,
    ABS(SUM(total_sales - cogs)) total_loss
FROM
    pharmacy_sales
WHERE
    total_sales - cogs < 0
GROUP BY
    manufacturer
ORDER BY
    total_loss DESC
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
