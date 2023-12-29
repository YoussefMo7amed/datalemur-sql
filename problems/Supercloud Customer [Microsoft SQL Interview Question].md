# Supercloud Customer [Microsoft SQL Interview Question]

- Problem level: Medium

- Company: Microsoft
- Problem Link: '[here](https://datalemur.com/questions/supercloud-customer?referralCode=256wYou1)'

---
<p>A Microsoft Azure Supercloud customer is defined as a company that purchases at least one product from each product category.</p>
<p>Write a query that effectively identifies the company ID of such Supercloud customers.</p>
<p><em>As of 5 Dec 2022, data in the <!-- --> and <!-- --> tables were updated.</em></p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">customer_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">amount</td><td style="text-align:left">integer</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">customer_id</th><th style="text-align:left">product_id</th><th style="text-align:left">amount</th></tr></thead><tbody><tr><td style="text-align:left">1</td><td style="text-align:left">1</td><td style="text-align:left">1000</td></tr><tr><td style="text-align:left">1</td><td style="text-align:left">3</td><td style="text-align:left">2000</td></tr><tr><td style="text-align:left">1</td><td style="text-align:left">5</td><td style="text-align:left">1500</td></tr><tr><td style="text-align:left">2</td><td style="text-align:left">2</td><td style="text-align:left">3000</td></tr><tr><td style="text-align:left">2</td><td style="text-align:left">6</td><td style="text-align:left">2000</td></tr></tbody></table></div>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">product_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">product_category</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">product_name</td><td style="text-align:left">string</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">product_id</th><th style="text-align:left">product_category</th><th style="text-align:left">product_name</th></tr></thead><tbody><tr><td style="text-align:left">1</td><td style="text-align:left">Analytics</td><td style="text-align:left">Azure Databricks</td></tr><tr><td style="text-align:left">2</td><td style="text-align:left">Analytics</td><td style="text-align:left">Azure Stream Analytics</td></tr><tr><td style="text-align:left">4</td><td style="text-align:left">Containers</td><td style="text-align:left">Azure Kubernetes Service</td></tr><tr><td style="text-align:left">5</td><td style="text-align:left">Containers</td><td style="text-align:left">Azure Service Fabric</td></tr><tr><td style="text-align:left">6</td><td style="text-align:left">Compute</td><td style="text-align:left">Virtual Machines</td></tr><tr><td style="text-align:left">7</td><td style="text-align:left">Compute</td><td style="text-align:left">Azure Functions</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">customer_id</th></tr></thead><tbody><tr><td style="text-align:left">1</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Customer 1 bought from Analytics, Containers, and Compute categories of Azure, and thus is a Supercloud customer. Customer 2 isn't a Supercloud customer, since they don't buy any container services from Azure.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

---

## Solutions

<details>
<summary> Solution </summary>
- Join the 2 tables on product_id
- count distinct category that each customer bought
- compare each user count with the total count of distinct category in products

```sql
with custmer_category_count as (
    SELECT
        customer_id,
        COUNT(DISTINCT product_category) categories
    FROM
        customer_contracts cc
        INNER JOIN products p ON cc.product_id = p.product_id
    GROUP BY
        customer_id
)
SELECT
    customer_id
FROM
    custmer_category_count
WHERE
    categories = (
        SELECT
            COUNT(DISTINCT product_category)
        FROM
            products
    )
```

</details>

<details>
<summary> Solution </summary>

```sql


```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
