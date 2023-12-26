# Highest-Grossing Items [Amazon SQL Interview Question]

- Problem level: Medium

- Company: Amazon
- Problem Link: '[here](https://datalemur.com/questions/sql-highest-grossing?referralCode=256wYou1)'

---
<p>This is the same question as problem #12 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you're given a table containing data on Amazon customers and their spending on products in different category, write a query to identify the top two highest-grossing products within each category in the year 2022. The output should include the category, product, and total spend.</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">category</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">product</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">spend</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">transaction_date</td><td style="text-align:left">timestamp</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">category</th><th style="text-align:left">product</th><th style="text-align:left">user_id</th><th style="text-align:left">spend</th><th style="text-align:left">transaction_date</th></tr></thead><tbody><tr><td style="text-align:left">appliance</td><td style="text-align:left">refrigerator</td><td style="text-align:left">165</td><td style="text-align:left">246.00</td><td style="text-align:left">12/26/2021 12:00:00</td></tr><tr><td style="text-align:left">appliance</td><td style="text-align:left">refrigerator</td><td style="text-align:left">123</td><td style="text-align:left">299.99</td><td style="text-align:left">03/02/2022 12:00:00</td></tr><tr><td style="text-align:left">appliance</td><td style="text-align:left">washing machine</td><td style="text-align:left">123</td><td style="text-align:left">219.80</td><td style="text-align:left">03/02/2022 12:00:00</td></tr><tr><td style="text-align:left">electronics</td><td style="text-align:left">vacuum</td><td style="text-align:left">178</td><td style="text-align:left">152.00</td><td style="text-align:left">04/05/2022 12:00:00</td></tr><tr><td style="text-align:left">electronics</td><td style="text-align:left">wireless headset</td><td style="text-align:left">156</td><td style="text-align:left">249.90</td><td style="text-align:left">07/08/2022 12:00:00</td></tr><tr><td style="text-align:left">electronics</td><td style="text-align:left">vacuum</td><td style="text-align:left">145</td><td style="text-align:left">189.00</td><td style="text-align:left">07/15/2022 12:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">category</th><th style="text-align:left">product</th><th style="text-align:left">total_spend</th></tr></thead><tbody><tr><td style="text-align:left">appliance</td><td style="text-align:left">refrigerator</td><td style="text-align:left">299.99</td></tr><tr><td style="text-align:left">appliance</td><td style="text-align:left">washing machine</td><td style="text-align:left">219.80</td></tr><tr><td style="text-align:left">electronics</td><td style="text-align:left">vacuum</td><td style="text-align:left">341.00</td></tr><tr><td style="text-align:left">electronics</td><td style="text-align:left">wireless headset</td><td style="text-align:left">249.90</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Within the "appliance" category, the top two highest-grossing products are "refrigerator" and "washing machine."</p>
<p>In the "electronics" category, the top two highest-grossing products are "vacuum" and "wireless headset."</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- Top 2 in each category

---

## Solutions

<details>
<summary> Solution </summary>

```sql
WITH CategoryRankedProducts AS (
    SELECT
        category,
        product,
        SUM(spend) AS total_spend,
        ROW_NUMBER() OVER (
            PARTITION BY category
            ORDER BY
                SUM(spend) DESC
        ) AS rnk
    FROM
        product_spend
    WHERE
        EXTRACT(
            YEAR
            FROM
                transaction_date
        ) = 2022
    GROUP BY
        category,
        product
)
SELECT
    category,
    product,
    total_spend
FROM
    CategoryRankedProducts
WHERE
    rnk <= 2;
```

1. ### Common Table Expression (CTE): CategoryRankedProducts

The query starts by creating a Common Table Expression (CTE) named CategoryRankedProducts.
Within this CTE, it selects the category, product, and the SUM of spend for each product within its category.
The WHERE clause filters the data to include only transactions from the year 2022.
The result is grouped by category and product to calculate the total spend for each product within its category.

2. ### Row Numbering with Window Function: ROW_NUMBER()

The ROW_NUMBER() window function is used within the CTE to assign a row number to each row within its category based on the total spend in descending order.
The PARTITION BY category clause ensures that the row numbering restarts for each category.
The ordering is done by the total spend in descending order (ORDER BY SUM(spend) DESC).

3. ### Final Query: Selecting Top Two Products

The outer query selects from the CategoryRankedProducts CTE.
It retrieves the category, product, and total_spend columns.
The WHERE rnk <= 2 condition ensures that only the rows where the row number is 1 or 2 (indicating the top two highest-grossing products within each category) are included in the final result.

</details>

---

### Follow up

What if i want top two highest-grossing products within each category *NOT the total spending* and don't care about which year.

<details>
<summary> Solution </summary>

```SQL
WITH BY_product AS (
    SELECT
        category,
        product,
        spend,
        ROW_NUMBER() OVER (
            PARTITION BY product
            ORDER BY
                spend DESC
        ) AS product_rnk
    FROM
        product_spend
),
by_category_product as(
    SELECT
        category,
        product,
        spend,
        ROW_NUMBER() OVER (
            PARTITION BY category
            ORDER BY
                spend DESC
        ) AS rnk
    from
        BY_product
    where
        product_rnk = 1
)
SELECT
    category,
    product,
    spend
FROM
    by_category_product
WHERE
    rnk <= 2;
```

</details>

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
