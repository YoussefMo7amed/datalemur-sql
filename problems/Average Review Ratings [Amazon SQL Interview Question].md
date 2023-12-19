# Average Review Ratings [Amazon SQL Interview Question]

- Problem level: Easy

- Company: Amazon
- Problem Link: '[here](https://datalemur.com/questions/sql-avg-review-ratings?referralCode=256wYou1)'

---
<p>Given the reviews table, write a query to retrieve the average star rating for each product, grouped by month. The output should display the month as a numerical value, product ID, and average star rating rounded to two decimal places. Sort the output first by month and then by product ID.</p>
<p>P.S. If you've read the <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>, and liked it, consider writing us a review?</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">review_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">submit_date</td><td style="text-align:left">datetime</td></tr><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">stars</td><td style="text-align:left">integer (1-5)</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>review_id</strong></th><th style="text-align:left"><strong>user_id</strong></th><th style="text-align:left"><strong>submit_date</strong></th><th style="text-align:left"><strong>product_id</strong></th><th style="text-align:left"><strong>stars</strong></th></tr></thead><tbody><tr><td style="text-align:left">6171</td><td style="text-align:left">123</td><td style="text-align:left">06/08/2022 00:00:00</td><td style="text-align:left">50001</td><td style="text-align:left">4</td></tr><tr><td style="text-align:left">7802</td><td style="text-align:left">265</td><td style="text-align:left">06/10/2022 00:00:00</td><td style="text-align:left">69852</td><td style="text-align:left">4</td></tr><tr><td style="text-align:left">5293</td><td style="text-align:left">362</td><td style="text-align:left">06/18/2022 00:00:00</td><td style="text-align:left">50001</td><td style="text-align:left">3</td></tr><tr><td style="text-align:left">6352</td><td style="text-align:left">192</td><td style="text-align:left">07/26/2022 00:00:00</td><td style="text-align:left">69852</td><td style="text-align:left">3</td></tr><tr><td style="text-align:left">4517</td><td style="text-align:left">981</td><td style="text-align:left">07/05/2022 00:00:00</td><td style="text-align:left">69852</td><td style="text-align:left">2</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>mth</strong></th><th style="text-align:left"><strong>product</strong></th><th style="text-align:left"><strong>avg_stars</strong></th></tr></thead><tbody><tr><td style="text-align:left">6</td><td style="text-align:left">50001</td><td style="text-align:left">3.50</td></tr><tr><td style="text-align:left">6</td><td style="text-align:left">69852</td><td style="text-align:left">4.00</td></tr><tr><td style="text-align:left">7</td><td style="text-align:left">69852</td><td style="text-align:left">2.50</td></tr></tbody></table></div>
<h3>Explanation</h3>
<p>Product 50001 received two ratings of 4 and 3 in the month of June (6th month), resulting in an average star rating of 3.5.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>
<h3>Want to try other Amazon SQL Interview Questions?</h3>
<p>Here's some more Amazon SQL Interview Questions:
<img alt="Amazon SQL Interview Questions" src="https://api.datalemur.com/assets/74d0a619-2138-4e73-bd02-91d5c02d208e"/></p>

---

## Notes

In SQL, the order of execution is important to understand. In the given solution's query, the sequence of execution is as follows:

1. **FROM** clause: The query fetches data from the `reviews` table.
2. **GROUP BY** clause: SQL performs grouping based on the `EXTRACT(MONTH FROM submit_date)` and `product_id` columns.
3. **SELECT** clause: The query selects the `EXTRACT(MONTH FROM submit_date)` column and aliases it as `mth`, along with the `product_id` and the average of stars rounded to two decimal places as `avg_stars`.
4. **ORDER BY** clause: The query sorts the results based on the `mth` column, which is the alias used in the SELECT clause, followed by the `product_id` column.

It's important to note that the `GROUP BY` clause is executed before the `SELECT` statement. Therefore, we cannot use the mth alias in the `GROUP BY` clause, as the mth column is created after the `SELECT` statement is executed. However, we can use the mth alias in the ORDER BY clause, as it is executed after the `SELECT` statement, and the mth column has been created by then.

Understanding the order of SQL execution is crucial, as it is a common topic in technical interviews. It's recommended to familiarize yourself with the sequence of execution in SQL for better query writing and debugging.

---

## Solutions

<details>
<summary> Solution </summary>

Refer to [this tutorial](https://datalemur.com/sql-tutorial/sql-date-time-function) for more explanation on the EXTRACT function.

```sql
SELECT
    EXTRACT(
        Month
        from
            submit_date
    ) mth,
    product_id product,
    ROUND(AVG(stars), 2) avg_stars
from
    reviews
group by
    EXTRACT(
        Month
        from
            submit_date
    ),
    product_id
ORDER BY
    EXTRACT(
        Month
        from
            submit_date
    ),
    product_id
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
