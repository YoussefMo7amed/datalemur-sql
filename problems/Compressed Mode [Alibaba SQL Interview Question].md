# Compressed Mode [Alibaba SQL Interview Question]

- Problem level: Medium

- Company: Alibaba
- Problem Link: '[here](https://datalemur.com/questions/alibaba-compressed-mode?referralCode=256wYou1)'

---
<p>You're given a table containing the item count for each order on Alibaba, along with the frequency of orders that have the same item count. Write a query to retrieve the mode of the order occurrences. Additionally, if there are multiple item counts with the same mode, the results should be sorted in ascending order.</p>
<p>Clarifications:</p>
<ul>
<li>: Represents the number of items sold in each order.</li>
<li>: Represents the frequency of orders with the corresponding number of items sold per order.</li>
<li>For example, if there are 800 orders with 3 items sold in each order, the record would have an <!-- --> of 3 and an <!-- --> of 800.</li>
</ul>
<p><em>Effective June 14th, 2023, the problem statement has been revised and additional clarification have been added for clarity.</em></p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">item_count</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">order_occurrences</td><td style="text-align:left">integer</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">item_count</th><th style="text-align:left">order_occurrences</th></tr></thead><tbody><tr><td style="text-align:left">1</td><td style="text-align:left">500</td></tr><tr><td style="text-align:left">2</td><td style="text-align:left">1000</td></tr><tr><td style="text-align:left">3</td><td style="text-align:left">800</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">mode</th></tr></thead><tbody><tr><td style="text-align:left">2</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Based on the example output, the <!-- --> value of 1000 corresponds to the highest frequency among all item counts. This means that item count of 2 has occurred 1000 times, making it the mode of order occurrences.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- Just get the max `order_occurrences` value then compare each one with it.

---

## Solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    item_count as mode
FROM
    items_per_order
where
    order_occurrences = (
        SELECT
            MAX(order_occurrences)
        from
            items_per_order
    )
ORDER BY
    mode
```

</details>

<details>
<summary> Solution 2 (website solution)</summary>
Using MODE() WITHIN GROUP ()

[for more info here](https://www.postgresql.org/docs/9.4/functions-aggregate.html#FUNCTIONS-ORDEREDSET-TABLE)

```sql
SELECT
    MODE() WITHIN GROUP (
        ORDER BY
            order_occurrences DESC
    )
FROM
    items_per_order;
```

</details>

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
