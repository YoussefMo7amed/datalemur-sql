# Laptop vs. Mobile Viewership [New York Times SQL Interview Question]

- Problem level: Easy

- Company: New York Times
- Problem Link: '[here](https://datalemur.com/questions/laptop-mobile-viewership)'

---
<p>This is the same question as problem #3 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you're given the table on user viewership categorised by device type where the three types are laptop, tablet, and phone.</p>
<p>Write a query that calculates the total viewership for laptops and mobile devices where mobile is defined as the sum of tablet and phone viewership. Output the total viewership for laptops as <!-- --> and the total viewership for mobile devices as <!-- -->.</p>
<p><em>Effective 15 April 2023, the solution has been updated with a more concise and easy-to-understand approach.</em></p>
<h3> Table</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">device_type</td><td style="text-align:left">string ('laptop', 'tablet', 'phone')</td></tr><tr><td style="text-align:left">view_time</td><td style="text-align:left">timestamp</td></tr></tbody></table></div>
<h3> Example Input</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">user_id</th><th style="text-align:left">device_type</th><th style="text-align:left">view_time</th></tr></thead><tbody><tr><td style="text-align:left">123</td><td style="text-align:left">tablet</td><td style="text-align:left">01/02/2022 00:00:00</td></tr><tr><td style="text-align:left">125</td><td style="text-align:left">laptop</td><td style="text-align:left">01/07/2022 00:00:00</td></tr><tr><td style="text-align:left">128</td><td style="text-align:left">laptop</td><td style="text-align:left">02/09/2022 00:00:00</td></tr><tr><td style="text-align:left">129</td><td style="text-align:left">phone</td><td style="text-align:left">02/09/2022 00:00:00</td></tr><tr><td style="text-align:left">145</td><td style="text-align:left">tablet</td><td style="text-align:left">02/24/2022 00:00:00</td></tr></tbody></table></div>
<h3>Example Output</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">laptop_views</th><th style="text-align:left">mobile_views</th></tr></thead><tbody><tr><td style="text-align:left">2</td><td style="text-align:left">3</td></tr></tbody></table></div>
<h3>Explanation</h3>
<p>Based on the example input, there are a total of 2 laptop views and 3 mobile views.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## Solutions

<details>
<summary> Solution 1</summary>

```sql
select
    (
        select
            count(1)
        from
            viewership
        where
            device_type = 'laptop'
    ) laptop_views,
    (
        select
            count(1)
        from
            viewership
        where
            device_type = 'phone'
            or device_type = 'tablet'
    ) mobile_views

```

</details>

website solutions:

<details>
<summary> Solution 2</summary>

Using [`FILTER`](https://modern-sql.com/feature/filter) function

```sql
SELECT
  COUNT(*) FILTER (WHERE conditional_expression)
FROM table_name;
```

```sql
SELECT 
  COUNT(*) FILTER (WHERE device_type = 'laptop') AS laptop_views,
  COUNT(*) FILTER (WHERE device_type IN ('tablet', 'phone'))  AS mobile_views 
FROM viewership;
```

</details>

<details>
<summary> Solution 3</summary>

Using `SUM()` & `CASE` statement

```sql
SELECT 
  SUM(CASE WHEN device_type = 'laptop' THEN 1 ELSE 0 END) AS laptop_views, 
  SUM(CASE WHEN device_type IN ('tablet', 'phone') THEN 1 ELSE 0 END) AS mobile_views 
FROM viewership;
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
