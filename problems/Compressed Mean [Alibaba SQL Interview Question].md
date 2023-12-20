# Compressed Mean [Alibaba SQL Interview Question]

- Problem level: Easy

- Company: Alibaba
- Problem Link: '[here](https://datalemur.com/questions/alibaba-compressed-mean?referralCode=256wYou1)'

---
<p>You're trying to find the mean number of items per order on Alibaba, rounded to 1 decimal place using tables which includes information on the count of items in each order (<!-- --> table) and the corresponding number of orders for each item count (<!-- --> table).</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">item_count</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">order_occurrences</td><td style="text-align:left">integer</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">item_count</th><th style="text-align:left">order_occurrences</th></tr></thead><tbody><tr><td style="text-align:left">1</td><td style="text-align:left">500</td></tr><tr><td style="text-align:left">2</td><td style="text-align:left">1000</td></tr><tr><td style="text-align:left">3</td><td style="text-align:left">800</td></tr><tr><td style="text-align:left">4</td><td style="text-align:left">1000</td></tr></tbody></table></div>
<p>There are a total of 500 orders with one item per order, 1000 orders with two items per order, and 800 orders with three items per order."</p>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">mean</th></tr></thead><tbody><tr><td style="text-align:left">2.7</td></tr></tbody></table></div>
<h2>Explanation</h2>
<p>Let's calculate the arithmetic average:</p>
<p>Total items = </p>
<p>Total orders = </p>
<p>Mean = </p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

Before the solution it worth noting that you can know the type of the result using `pg_typeof` function

```sql
SELECT
    pg_typeof(SUM(item_count * order_occurrences)) AS result_type
FROM
    items_per_order;

```

the output of this query is

```bash
double precision
```

In PostgreSQL 14
`ROUND` function doesn't accept `double precision` type

if you try

```sql
select ROUND(5::double precision,1)
```

you will get

``
function round(double precision, integer) does not exist (LINE: 1)
``

so you need to cast it into `NUMERIC` or `DECIMAL` type with `::` or `CAST(field AS TYPE)` like `CAST(field AS DECIMAL)` OR `::DECIMAL`

---

## Solutions

<details>
<summary> Solution </summary>

Read the notes above for more clarification

```sql
SELECT
    ROUND(
        SUM(item_count * order_occurrences) :: DECIMAL / (
            SELECT
                SUM(order_occurrences)
            from
                items_per_order
        ),
        1
    ) AS mean
FROM
    items_per_order
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
