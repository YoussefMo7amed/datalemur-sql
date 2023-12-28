# Signup Activation Rate [TikTok SQL Interview Question]

- Problem level: Medium

- Company: TikTok
- Problem Link: '[here](https://datalemur.com/questions/signup-confirmation-rate?referralCode=256wYou1)'

---
<p>New TikTok users sign up with their emails. They confirmed their signup by replying to the text confirmation to activate their accounts. Users may receive multiple text messages for account confirmation until they have confirmed their new account.</p>
<p>A senior analyst is interested to know the activation rate of specified users in the <!-- --> table. Write a query to find the activation rate. Round the percentage to 2 decimal places.</p>
<p>Definitions:</p>
<ul>
<li> table contain the information of user signup details.</li>
<li> table contains the users' activation information.</li>
</ul>
<p>Assumptions:</p>
<ul>
<li>The analyst is interested in the activation rate of specific users in the <!-- --> table, which may not include all users that could potentially be found in the <!-- --> table.</li>
<li>For example, user 123 in the <!-- --> table may not be in the <!-- --> table and vice versa.</li>
</ul>
<p><em>Effective April 4th 2023, we added an assumption to the question to provide additional clarity.</em></p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">email_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">signup_date</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>email_id</strong></th><th style="text-align:left"><strong>user_id</strong></th><th style="text-align:left"><strong>signup_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">125</td><td style="text-align:left">7771</td><td style="text-align:left">06/14/2022 00:00:00</td></tr><tr><td style="text-align:left">236</td><td style="text-align:left">6950</td><td style="text-align:left">07/01/2022 00:00:00</td></tr><tr><td style="text-align:left">433</td><td style="text-align:left">1052</td><td style="text-align:left">07/09/2022 00:00:00</td></tr></tbody></table></div>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">text_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">email_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">signup_action</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>text_id</strong></th><th style="text-align:left"><strong>email_id</strong></th><th style="text-align:left"><strong>signup_action</strong></th></tr></thead><tbody><tr><td style="text-align:left">6878</td><td style="text-align:left">125</td><td style="text-align:left">Confirmed</td></tr><tr><td style="text-align:left">6920</td><td style="text-align:left">236</td><td style="text-align:left">Not Confirmed</td></tr><tr><td style="text-align:left">6994</td><td style="text-align:left">236</td><td style="text-align:left">Confirmed</td></tr></tbody></table></div>
<p>'Confirmed' in <!-- --> means the user has activated their account and successfully completed the signup process.</p>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>confirm_rate</strong></th></tr></thead><tbody><tr><td style="text-align:left">0.67</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>67% of users have successfully completed their signup and activated their accounts. The remaining 33% have not yet replied to the text to confirm their signup.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

---

## Solutions

<details>
<summary> Solution </summary>

```sql
with count_uniques as (
    SELECT
        COUNT(1) ids
    from
        emails e FULL
        OUTER JOIN texts t on e.email_id = t.email_id
    where
        e.email_id is NULL
        OR t.email_id is NULL
),
count_all_ids as (
    SELECT
        COUNT(DISTINCT email_id) ids
    from
        (
            SELECT
                email_id
            from
                emails
            UNION
            SELECT
                email_id
            from
                texts
        ) ids
)
SELECT
    ROUND(
        (
            select
                ids
            from
                count_uniques
        ) :: decimal /(
            SELECT
                ids
            from
                count_all_ids
        ) :: decimal,
        2
    ) confirm_rate
```

</details>

<details>
<summary> Solution (from website) </summary>
Step 1: Join tables for records with successful confirmations
To start, we will use a LEFT JOIN to connect the emails and texts tables. It's important to note that an INNER JOIN won't work for this question and we'll explain why shortly.

We'll keep only the users who successfully signed up and received a 'Confirmed' text confirmation in the signup_action column located in the texts table.

```sql
SELECT
    texts.email_id,
    emails.email_id
FROM
    emails
    LEFT JOIN texts ON emails.email_id = texts.email_id
    AND texts.signup_action = 'Confirmed';
```

Your output should look something like this:

email_id email_id
125 125
236 236
433
450
Why LEFT JOIN is Necessary in this Query?

Now, it's important to note that not every email_id in the emails table will have a matching value in the texts table, and this is where the LEFT JOIN comes into play.

When we perform a LEFT JOIN, all the rows from the left table (emails in this case) are returned along with matching rows from the right table (texts in this case). If there is no match for a particular row in the right table, then the columns from the right table will be NULL.

If we were to use an INNER JOIN, only the matching rows between the two tables would be returned, effectively filtering out any email_id values from the emails table that do not have a corresponding match in the texts table.

Output from using an INNER JOIN:

email_id email_id
125 125
236 236
This could result in relevant users being excluded from the calculation completely, which is not what we want.

Step 2: Calculate the signup activation rate of users who have confirmed their accounts
Signup Activation Rate = Number of users who confirmed their accounts / Number of users in the emails table

With the given formula, we expressed them in the query below.

```sql
SELECT
    COUNT(texts.email_id) / COUNT(DISTINCT emails.email_id) AS activation_rate
FROM
    emails
    LEFT JOIN texts ON emails.email_id = texts.email_id
    AND texts.signup_action = 'Confirmed';
```

But wait, did you get an activation rate of '0' when you ran the query? That's because dividing an integer with another integer would sometimes result in '0'.

To avoid this, we'll need to cast either the denominator or the numerator to DECIMAL type.

Finally, the ROUND() function is used to truncate the result to 2 decimal places, as specified in the instructions.

```sql
SELECT
    ROUND(
        COUNT(texts.email_id) :: DECIMAL / COUNT(DISTINCT emails.email_id),
        2
    ) AS activation_rate
FROM
    emails
    LEFT JOIN texts ON emails.email_id = texts.email_id
    AND texts.signup_action = 'Confirmed';
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
