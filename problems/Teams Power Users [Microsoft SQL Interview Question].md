# Teams Power Users [Microsoft SQL Interview Question]

- Problem level: Easy

- Company: Microsoft
- Problem Link: '[here](https://datalemur.com/questions/teams-power-users)'

---
<p>Write a query to identify the top 2 Power Users who sent the highest number of messages on Microsoft Teams in August 2022. Display the IDs of these 2 users along with the total number of messages they sent. Output the results in descending order based on the count of the messages.</p>
<p>Assumption:</p>
<ul>
<li>No two users have sent the same number of messages in August 2022.</li>
</ul>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">message_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">sender_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">receiver_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">content</td><td style="text-align:left">varchar</td></tr><tr><td style="text-align:left">sent_date</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>message_id</strong></th><th style="text-align:left"><strong>sender_id</strong></th><th style="text-align:left"><strong>receiver_id</strong></th><th style="text-align:left"><strong>content</strong></th><th style="text-align:left"><strong>sent_date</strong></th></tr></thead><tbody><tr><td style="text-align:left">901</td><td style="text-align:left">3601</td><td style="text-align:left">4500</td><td style="text-align:left">You up?</td><td style="text-align:left">08/03/2022 00:00:00</td></tr><tr><td style="text-align:left">902</td><td style="text-align:left">4500</td><td style="text-align:left">3601</td><td style="text-align:left">Only if you're buying</td><td style="text-align:left">08/03/2022 00:00:00</td></tr><tr><td style="text-align:left">743</td><td style="text-align:left">3601</td><td style="text-align:left">8752</td><td style="text-align:left">Let's take this offline</td><td style="text-align:left">06/14/2022 00:00:00</td></tr><tr><td style="text-align:left">922</td><td style="text-align:left">3601</td><td style="text-align:left">4500</td><td style="text-align:left">Get on the call</td><td style="text-align:left">08/10/2022 00:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>sender_id</strong></th><th style="text-align:left"><strong>message_count</strong></th></tr></thead><tbody><tr><td style="text-align:left">3601</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">4500</td><td style="text-align:left">1</td></tr></tbody></table></div>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

Just turn it into sub-problems

---

## Solutions

<details>
<summary> Solution </summary>

```sql
SELECT
    sender_id,
    count(1) message_count
FROM
    messages
WHERE
    EXTRACT(
        Month
        from
            sent_date
    ) = 8
    and EXTRACT(
        year
        from
            sent_date
    ) = 2022
GROUP BY
    sender_id
ORDER BY
    message_count DESC
LIMIT
    2
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
