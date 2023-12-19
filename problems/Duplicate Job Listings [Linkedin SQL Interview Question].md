# Duplicate Job Listings [Linkedin SQL Interview Question]

- Problem level: Easy

- Company: Linkedin
- Problem Link: '[here](https://datalemur.com/questions/duplicate-job-listings?referralCode=256wYou1)'

---
<p>This is the same question as problem #8 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you're given a table containing job postings from various companies on the LinkedIn platform. Write a query to retrieve the count of companies that have posted duplicate job listings.</p>
<p>Definition:</p>
<ul>
<li>Duplicate job listings are defined as two job listings within the same company that share identical titles and descriptions.</li>
</ul>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">job_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">company_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">title</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">description</td><td style="text-align:left">string</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">job_id</th><th style="text-align:left">company_id</th><th style="text-align:left">title</th><th style="text-align:left">description</th></tr></thead><tbody><tr><td style="text-align:left">248</td><td style="text-align:left">827</td><td style="text-align:left">Business Analyst</td><td style="text-align:left">Business analyst evaluates past and current business data with the primary goal of improving decision-making processes within organizations.</td></tr><tr><td style="text-align:left">149</td><td style="text-align:left">845</td><td style="text-align:left">Business Analyst</td><td style="text-align:left">Business analyst evaluates past and current business data with the primary goal of improving decision-making processes within organizations.</td></tr><tr><td style="text-align:left">945</td><td style="text-align:left">345</td><td style="text-align:left">Data Analyst</td><td style="text-align:left">Data analyst reviews data to identify key insights into a business's customers and ways the data can be used to solve problems.</td></tr><tr><td style="text-align:left">164</td><td style="text-align:left">345</td><td style="text-align:left">Data Analyst</td><td style="text-align:left">Data analyst reviews data to identify key insights into a business's customers and ways the data can be used to solve problems.</td></tr><tr><td style="text-align:left">172</td><td style="text-align:left">244</td><td style="text-align:left">Data Engineer</td><td style="text-align:left">Data engineer works in a variety of settings to build systems that collect, manage, and convert raw data into usable information for data scientists and business analysts to interpret.</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">duplicate_companies</th></tr></thead><tbody><tr><td style="text-align:left">1</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>There is one company ID 345 that posted duplicate job listings. The duplicate listings, IDs 945 and 164 have identical titles and descriptions.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

---

## Solutions

<details>
<summary> Solution </summary>

```sql
-- we divided by 2 since each job will be repeated twice (when it compares itself with other job, and other job compare itself with it.)
SELECT
    COUNT(1)/2 duplicate_companies
from
    job_listings jl
    join job_listings jl2 on jl.company_id = jl2.company_id
    and jl.title = jl2.title
    and jl.description = jl2.description
where
    jl.job_id != jl2.job_id

```

</details>

website solutions

<details>
<summary> Solution 2 </summary>

Step 1: Identify companies with duplicate job listings
Step 2: Filter for companies with duplicate job listings

```sql
WITH job_count_cte AS (
    SELECT
        company_id,
        title,
        description,
        COUNT(job_id) AS job_count
    FROM
        job_listings
    GROUP BY
        company_id,
        title,
        description
)
SELECT
    COUNT(DISTINCT company_id) AS duplicate_companies
FROM
    job_count_cte
WHERE
    job_count > 1;
```

</details>

<details>
<summary> Solution 3 </summary>

```sql
SELECT
    COUNT(DISTINCT company_id) AS duplicate_companies
FROM
    (
        SELECT
            company_id,
            title,
            description,
            COUNT(job_id) AS job_count
        FROM
            job_listings
        GROUP BY
            company_id,
            title,
            description
    ) AS job_count_cte
WHERE
    job_count > 1;
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
