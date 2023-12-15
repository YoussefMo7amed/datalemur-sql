# Page With No Likes [Facebook SQL Interview Question]

- Problem level: Easy

- Company: Facebook
- Problem Link: '[here](https://datalemur.com/questions/sql-page-with-no-likes)'

---
<p>Assume you're given two tables containing data about Facebook Pages and their respective likes (as in "Like a Facebook Page").</p>
<p>Write a query to return the IDs of the Facebook pages that have zero likes. The output should be sorted in ascending order based on the page IDs.</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">page_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">page_name</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>page_id</strong></th><th style="text-align:left"><strong>page_name</strong></th></tr></thead><tbody><tr><td style="text-align:left">20001</td><td style="text-align:left">SQL Solutions</td></tr><tr><td style="text-align:left">20045</td><td style="text-align:left">Brain Exercises</td></tr><tr><td style="text-align:left">20701</td><td style="text-align:left">Tips for Data Analysts</td></tr></tbody></table></div>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">page_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">liked_date</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>user_id</strong></th><th style="text-align:left"><strong>page_id</strong></th><th style="text-align:left"><strong>liked_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">111</td><td style="text-align:left">20001</td><td style="text-align:left">04/08/2022 00:00:00</td></tr><tr><td style="text-align:left">121</td><td style="text-align:left">20045</td><td style="text-align:left">03/12/2022 00:00:00</td></tr><tr><td style="text-align:left">156</td><td style="text-align:left">20001</td><td style="text-align:left">07/25/2022 00:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>page_id</strong></th></tr></thead><tbody><tr><td style="text-align:left">20701</td></tr></tbody></table></div>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>
<p>p.s. If you have literally no idea how to solve this, maybe give our <a href="https://datalemur.com/sql-tutorial" rel="noopener noreferrer" target="_blank">free SQL tutorial</a> a try first?</p>

---

## Solutions

<details>
<summary> Solution 1</summary>

Using sub-query with `IN`

```sql
SELECT
    page_id
FROM
    pages
WHERE
    page_id NOT IN (
        SELECT
            page_id
        FROM
            page_likes
    )
ORDER BY
    page_id

```

</details>

<details>
<summary> Solution 2</summary>

Using `except`

```sql
SELECT
    page_id
FROM
    pages
except
SELECT
    page_id
FROM
    page_likes
ORDER BY
    page_id

```

</details>

<details>
<summary> Solution 3</summary>

Using sub-query with `EXISTS`

```sql
SELECT
    page_id
FROM
    pages
WHERE
    NOT EXISTS (
        SELECT
            page_id
        FROM
            page_likes AS likes
        WHERE
            likes.page_id = pages.page_id;

)
```

</details>

<details>
<summary> Solution 4</summary>

Using left join

```sql
SELECT
    p.page_id
FROM
    pages p
    LEFT OUTER JOIN page_likes AS l ON p.page_id = l.page_id
WHERE
    l.page_id IS NULL
ORDER BY
    p.page_id
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
