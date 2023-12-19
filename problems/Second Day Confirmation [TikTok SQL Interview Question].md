# Second Day Confirmation [TikTok SQL Interview Question]

- Problem level: Easy

- Company: TikTok
- Problem Link: '[here](https://datalemur.com/questions/second-day-confirmation?referralCode=256wYou1)'

---
<p>Assume you're given tables with information about TikTok user sign-ups and confirmations through email and text. New users on TikTok sign up using their email addresses, and upon sign-up, each user receives a text message confirmation to activate their account.</p>
<p>Write a query to display the user IDs of those who did not confirm their sign-up on the first day, but confirmed on the second day.</p>
<p>Definition:</p>
<ul>
<li> refers to the date when users activated their accounts and confirmed their sign-up through text messages.</li>
</ul>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">email_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">signup_date</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>email_id</strong></th><th style="text-align:left"><strong>user_id</strong></th><th style="text-align:left"><strong>signup_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">125</td><td style="text-align:left">7771</td><td style="text-align:left">06/14/2022 00:00:00</td></tr><tr><td style="text-align:left">433</td><td style="text-align:left">1052</td><td style="text-align:left">07/09/2022 00:00:00</td></tr></tbody></table></div>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">text_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">email_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">signup_action</td><td style="text-align:left">string ('Confirmed', 'Not confirmed')</td></tr><tr><td style="text-align:left">action_date</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>text_id</strong></th><th style="text-align:left"><strong>email_id</strong></th><th style="text-align:left"><strong>signup_action</strong></th><th style="text-align:left"><strong>action_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">6878</td><td style="text-align:left">125</td><td style="text-align:left">Confirmed</td><td style="text-align:left">06/14/2022 00:00:00</td></tr><tr><td style="text-align:left">6997</td><td style="text-align:left">433</td><td style="text-align:left">Not Confirmed</td><td style="text-align:left">07/09/2022 00:00:00</td></tr><tr><td style="text-align:left">7000</td><td style="text-align:left">433</td><td style="text-align:left">Confirmed</td><td style="text-align:left">07/10/2022 00:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>user_id</strong></th></tr></thead><tbody><tr><td style="text-align:left">1052</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Only User 1052 confirmed their sign-up on the second day.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- we want the date in `emails` table with the next day to it in `texts` table
- *Question* could user confirms the email more than one time? (should we handle this issue?)

---

## Solutions

<details>
<summary> Solution </summary>

- We can do calculations on dates using [`INTERVAL`](https://reintech.io/blog/sql-interval-data-type-detailed-guide)
- Notice that you can join 2 (or more) tables on more than one condition

```sql
SELECT
    DISTINCT user_id
FROM
    emails e
    INNER JOIN texts t ON e.email_id = t.email_id
    AND e.signup_date + INTERVAL '1 day' = t.action_date
WHERE
    signup_action = 'Confirmed'
```

</details>

website solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    DISTINCT user_id
FROM
    emails
    INNER JOIN texts ON emails.email_id = texts.email_id
WHERE
    texts.action_date = emails.signup_date + INTERVAL '1 day'
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
