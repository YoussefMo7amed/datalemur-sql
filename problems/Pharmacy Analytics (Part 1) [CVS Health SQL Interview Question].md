# Pharmacy Analytics (Part 1) [CVS Health SQL Interview Question]

- Problem level: Easy

- Company: CVS Health
- Problem Link: '[here](https://datalemur.com/questions/top-profitable-drugs?referralCode=256wYou1)'

---
<p>CVS Health is trying to better understand its pharmacy sales, and how well different products are selling. Each drug can only be produced by one manufacturer.</p>
<p>Write a query to find the top 3 most profitable drugs sold, and how much profit they made. Assume that there are no ties in the profits. Display the result from the highest to the lowest total profit.</p>
<p><strong>Definition:</strong></p>
<ul>
<li> stands for Cost of Goods Sold which is the direct cost associated with producing the drug.</li>
<li>Total Profit = Total Sales - Cost of Goods Sold</li>
</ul>
<p>If you like this question, try out <a href="https://datalemur.com/questions/non-profitable-drugs" rel="noopener noreferrer" target="_blank">Pharmacy Analytics (Part 2)</a>!</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">units_sold</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">total_sales</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">cogs</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">manufacturer</td><td style="text-align:left">varchar</td></tr><tr><td style="text-align:left">drug</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>product_id</strong></th><th style="text-align:left"><strong>units_sold</strong></th><th style="text-align:left"><strong>total_sales</strong></th><th style="text-align:left"><strong>cogs</strong></th><th style="text-align:left"><strong>manufacturer</strong></th><th style="text-align:left"><strong>drug</strong></th></tr></thead><tbody><tr><td style="text-align:left">9</td><td style="text-align:left">37410</td><td style="text-align:left">293452.54</td><td style="text-align:left">208876.01</td><td style="text-align:left">Eli Lilly</td><td style="text-align:left">Zyprexa</td></tr><tr><td style="text-align:left">34</td><td style="text-align:left">94698</td><td style="text-align:left">600997.19</td><td style="text-align:left">521182.16</td><td style="text-align:left">AstraZeneca</td><td style="text-align:left">Surmontil</td></tr><tr><td style="text-align:left">61</td><td style="text-align:left">77023</td><td style="text-align:left">500101.61</td><td style="text-align:left">419174.97</td><td style="text-align:left">Biogen</td><td style="text-align:left">Varicose Relief</td></tr><tr><td style="text-align:left">136</td><td style="text-align:left">144814</td><td style="text-align:left">1084258</td><td style="text-align:left">1006447.73</td><td style="text-align:left">Biogen</td><td style="text-align:left">Burkhart</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>drug</strong></th><th style="text-align:left"><strong>total_profit</strong></th></tr></thead><tbody><tr><td style="text-align:left">Zyprexa</td><td style="text-align:left">84576.53</td></tr><tr><td style="text-align:left">Varicose Relief</td><td style="text-align:left">80926.64</td></tr><tr><td style="text-align:left">Surmontil</td><td style="text-align:left">79815.03</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Zyprexa made the most profit (of $84,576.53) followed by Varicose Relief (of $80,926.64) and Surmontil (of $79,815.3).</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- Total Profit = Total Sales - Cost of Goods Sold
- Just take care of sorting and limit the results

---

## Solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    drug,
    total_sales - cogs AS total_profit
from
    pharmacy_sales
ORDER BY
    total_profit DESC
limit
    3
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
