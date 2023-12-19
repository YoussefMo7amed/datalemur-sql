# Cities With Completed Trades [Robinhood SQL Interview Question]

- Problem level: Easy

- Company: Robinhood
- Problem Link: '[here](https://datalemur.com/questions/completed-trades?referralCode=256wYou1)'

---
<p>This is the same question as problem #2 in the SQL Chapter of <a href="https://amzn.to/3kF79Fx" rel="noopener noreferrer" target="_blank">Ace the Data Science Interview</a>!</p>
<p>Assume you're given the tables containing completed trade orders and user details in a Robinhood trading system.</p>
<p>Write a query to retrieve the top three cities that have the highest number of completed trade orders listed in descending order. Output the city name and the corresponding number of completed trade orders.</p>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">order_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">price</td><td style="text-align:left">decimal</td></tr><tr><td style="text-align:left">quantity</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">status</td><td style="text-align:left">string('Completed' ,'Cancelled')</td></tr><tr><td style="text-align:left">timestamp</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">order_id</th><th style="text-align:left">user_id</th><th style="text-align:left">price</th><th style="text-align:left">quantity</th><th style="text-align:left">status</th><th style="text-align:left">timestamp</th></tr></thead><tbody><tr><td style="text-align:left">100101</td><td style="text-align:left">111</td><td style="text-align:left">9.80</td><td style="text-align:left">10</td><td style="text-align:left">Cancelled</td><td style="text-align:left">08/17/2022 12:00:00</td></tr><tr><td style="text-align:left">100102</td><td style="text-align:left">111</td><td style="text-align:left">10.00</td><td style="text-align:left">10</td><td style="text-align:left">Completed</td><td style="text-align:left">08/17/2022 12:00:00</td></tr><tr><td style="text-align:left">100259</td><td style="text-align:left">148</td><td style="text-align:left">5.10</td><td style="text-align:left">35</td><td style="text-align:left">Completed</td><td style="text-align:left">08/25/2022 12:00:00</td></tr><tr><td style="text-align:left">100264</td><td style="text-align:left">148</td><td style="text-align:left">4.80</td><td style="text-align:left">40</td><td style="text-align:left">Completed</td><td style="text-align:left">08/26/2022 12:00:00</td></tr><tr><td style="text-align:left">100305</td><td style="text-align:left">300</td><td style="text-align:left">10.00</td><td style="text-align:left">15</td><td style="text-align:left">Completed</td><td style="text-align:left">09/05/2022 12:00:00</td></tr><tr><td style="text-align:left">100400</td><td style="text-align:left">178</td><td style="text-align:left">9.90</td><td style="text-align:left">15</td><td style="text-align:left">Completed</td><td style="text-align:left">09/09/2022 12:00:00</td></tr><tr><td style="text-align:left">100565</td><td style="text-align:left">265</td><td style="text-align:left">25.60</td><td style="text-align:left">5</td><td style="text-align:left">Completed</td><td style="text-align:left">12/19/2022 12:00:00</td></tr></tbody></table></div>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">Column Name</th><th style="text-align:left">Type</th></tr></thead><tbody><tr><td style="text-align:left">user_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">city</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">email</td><td style="text-align:left">string</td></tr><tr><td style="text-align:left">signup_date</td><td style="text-align:left">datetime</td></tr></tbody></table></div>
<h3> Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">user_id</th><th style="text-align:left">city</th><th style="text-align:left">email</th><th style="text-align:left">signup_date</th></tr></thead><tbody><tr><td style="text-align:left">111</td><td style="text-align:left">San Francisco</td><td style="text-align:left"><a href="mailto:rrok10@gmail.com" target="_self">rrok10@gmail.com</a></td><td style="text-align:left">08/03/2021 12:00:00</td></tr><tr><td style="text-align:left">148</td><td style="text-align:left">Boston</td><td style="text-align:left"><a href="mailto:sailor9820@gmail.com" target="_self">sailor9820@gmail.com</a></td><td style="text-align:left">08/20/2021 12:00:00</td></tr><tr><td style="text-align:left">178</td><td style="text-align:left">San Francisco</td><td style="text-align:left"><a href="mailto:harrypotterfan182@gmail.com" target="_self">harrypotterfan182@gmail.com</a></td><td style="text-align:left">01/05/2022 12:00:00</td></tr><tr><td style="text-align:left">265</td><td style="text-align:left">Denver</td><td style="text-align:left"><a href="mailto:shadower_@hotmail.com" target="_self">shadower_@hotmail.com</a></td><td style="text-align:left">02/26/2022 12:00:00</td></tr><tr><td style="text-align:left">300</td><td style="text-align:left">San Francisco</td><td style="text-align:left"><a href="mailto:houstoncowboy1122@hotmail.com" target="_self">houstoncowboy1122@hotmail.com</a></td><td style="text-align:left">06/30/2022 12:00:00</td></tr></tbody></table></div>
<h3>Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left">city</th><th style="text-align:left">total_orders</th></tr></thead><tbody><tr><td style="text-align:left">San Francisco</td><td style="text-align:left">3</td></tr><tr><td style="text-align:left">Boston</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">Denver</td><td style="text-align:left">1</td></tr></tbody></table></div>
<h3>Explanation</h3>
<p>In the given dataset, San Francisco has the highest number of completed trade orders with 3 orders. Boston holds the second position with 2 orders, and Denver ranks third with 1 order.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- Note that we interested in 2 things:
  - City which in `users` table
  - total orders which we get from `trades` table
so we need a way to connect them (join them)
- we are interested in each city not total of all (grouping)

---

## Solutions

<details>
<summary> Solution </summary>

```sql
select
    city,
    count(u.user_id) total_orders
from
    users u
    inner join trades t on u.user_id = t.user_id
where
    status = 'Completed'
GROUP BY
    city
ORDER BY
    count(u.user_id) DESC
LIMIT
    3
```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
