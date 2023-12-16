# Average Post Hiatus (Part 1) [Facebook SQL Interview Question]

- Problem level: Easy

- Company: Facebook
- Problem Link: '[here](https://datalemur.com/questions/sql-average-post-hiatus-1)'

---
<p>Given a table of Facebook posts, for each user who posted at least twice in 2021, write a query to find the number of days between each user’s first post of the year and last post of the year in the year 2021. Output the user and number of the days between each user's first and last post.</p>
<p>p.s. If you've read the <a href="https://www.amazon.com/dp/0578973839?ref_=pe_3052080_397514860" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a> and liked it, consider writing us a review?</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">post_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">post_date</td><td style="text-align:left">timestamp</td></tr><tr><td style="text-align:left">post_content</td><td style="text-align:left">text</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">user_id</th><th style="text-align:left">post_id</th><th style="text-align:left">post_date</th><th style="text-align:left">post_content</th></tr></thead><tbody><tr><td style="text-align:left">151652</td><td style="text-align:left">599415</td><td style="text-align:left">07/10/2021 12:00:00</td><td style="text-align:left">Need a hug</td></tr><tr><td style="text-align:left">661093</td><td style="text-align:left">624356</td><td style="text-align:left">07/29/2021 13:00:00</td><td style="text-align:left">Bed. Class 8-12. Work 12-3. Gym 3-5 or 6. Then class 6-10. Another day that's gonna fly by. I miss my girlfriend</td></tr><tr><td style="text-align:left">004239</td><td style="text-align:left">784254</td><td style="text-align:left">07/04/2021 11:00:00</td><td style="text-align:left">Happy 4th of July!</td></tr><tr><td style="text-align:left">661093</td><td style="text-align:left">442560</td><td style="text-align:left">07/08/2021 14:00:00</td><td style="text-align:left">Just going to cry myself to sleep after watching Marley and Me.</td></tr><tr><td style="text-align:left">151652</td><td style="text-align:left">111766</td><td style="text-align:left">07/12/2021 19:00:00</td><td style="text-align:left">I'm so done with covid - need travelling ASAP!</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">user_id</th><th style="text-align:left">days_between</th></tr></thead><tbody><tr><td style="text-align:left">151652</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">661093</td><td style="text-align:left">21</td></tr></tbody></table></div>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

Thinking as i am a user:

- I have an ID
- Each post i post has a post_ID, content and date, i don't care about the content or post_ID
- Now i want my first and last post `date`, but in year 2021
  - so i want min(date) and max(date) in year 2021
- Do same for each user (group)

---

## Solutions

<details>
<summary> Solution 1</summary>
- Here i used [`EXTRACT()`](https://www.postgresqltutorial.com/postgresql-date-functions/postgresql-extract/) function
    - You can also use `DATE_PART()`
- You can subtract dates from each other using `-` or using

```sql
SELECT
    user_id,
    EXTRACT(
        DAY
        FROM
            MAX(post_date) - MIN(post_date)
    ) as days_between
from
    posts
WHERE
    EXTRACT(
        YEAR
        FROM
            post_date
    ) = 2021
group by
    user_id
HAVING
    COUNT(post_id) > 1;
```

</details>

website solutions

<details>
<summary> Solution 2</summary>

```sql
SELECT 
 user_id, 
    MAX(post_date::DATE) - MIN(post_date::DATE) AS days_between
FROM posts
WHERE DATE_PART('year', post_date::DATE) = 2021 
GROUP BY user_id
HAVING COUNT(post_id)>1;

```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
