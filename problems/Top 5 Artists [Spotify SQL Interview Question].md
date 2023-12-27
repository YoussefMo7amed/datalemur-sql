# Top 5 Artists [Spotify SQL Interview Question]

- Problem level: Medium

- Company: Spotify
- Problem Link: '[here](https://datalemur.com/questions/top-fans-rank?referralCode=256wYou1)'

---
<p>Assume there are three Spotify tables: `artists`, `songs`, and `global_song_rank` which contain information about the artists, songs, and music charts, respectively.</p>
<p>Write a query to find the top 5 artists whose songs appear most frequently in the Top 10 of the `global_song_rank` table. Display the top 5 artist names in ascending order, along with their song appearance ranking.</p>
<p>If two or more artists have the same number of song appearances, they should be assigned the same ranking, and the rank numbers should be continuous (i.e. 1, 2, 2, 3, 4, 5). If you've never seen a rank order like this before, do the <a href="https://datalemur.com/sql-tutorial/sql-rank-dense_rank-row_number-window-function" rel="noopener noreferrer" target="_blank">rank window function tutorial</a>.</p>
<h3> artists Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">artist_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">artist_name</td><td style="text-align:left">varchar</td></tr><tr><td style="text-align:left">label_owner</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3>artists Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th><strong>artist_id</strong></th><th><strong>artist_name</strong></th><th><strong>label_owner</strong></th></tr></thead><tbody><tr><td>101</td><td>Ed Sheeran</td><td>Warner Music Group</td></tr><tr><td>120</td><td>Drake</td><td>Warner Music Group</td></tr><tr><td>125</td><td>Bad Bunny</td><td>Rimas Entertainment</td></tr></tbody></table></div>
<h3>songs Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">song_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">artist_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">name</td><td style="text-align:left">varchar</td></tr></tbody></table></div>
<h3>songs Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th><strong>song_id</strong></th><th><strong>artist_id</strong></th><th><strong>name</strong></th></tr></thead><tbody><tr><td>55511</td><td>101</td><td>Perfect</td></tr><tr><td>45202</td><td>101</td><td>Shape of You</td></tr><tr><td>22222</td><td>120</td><td>One Dance</td></tr><tr><td>19960</td><td>120</td><td>Hotline Bling</td></tr></tbody></table></div>
<h3> Table:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>Column Name</strong></th><th style="text-align:left"><strong>Type</strong></th></tr></thead><tbody><tr><td style="text-align:left">day</td><td style="text-align:left">integer (1-52)</td></tr><tr><td style="text-align:left">song_id</td><td style="text-align:left">integer</td></tr><tr><td style="text-align:left">rank</td><td style="text-align:left">integer (1-1,000,000)</td></tr></tbody></table></div>
<h3>global_song_rank Example Input:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>day</strong></th><th style="text-align:left"><strong>song_id</strong></th><th style="text-align:left"><strong>rank</strong></th></tr></thead><tbody><tr><td style="text-align:left">1</td><td style="text-align:left">45202</td><td style="text-align:left">5</td></tr><tr><td style="text-align:left">3</td><td style="text-align:left">45202</td><td style="text-align:left">2</td></tr><tr><td style="text-align:left">1</td><td style="text-align:left">19960</td><td style="text-align:left">3</td></tr><tr><td style="text-align:left">9</td><td style="text-align:left">19960</td><td style="text-align:left">15</td></tr></tbody></table></div>
<h3> Example Output:</h3>
<div style="overflow-x:auto;margin-bottom:10px"><table><thead><tr><th style="text-align:left"><strong>artist_name</strong></th><th style="text-align:left"><strong>artist_rank</strong></th></tr></thead><tbody><tr><td style="text-align:left">Ed Sheeran</td><td style="text-align:left">1</td></tr><tr><td style="text-align:left">Drake</td><td style="text-align:left">2</td></tr></tbody></table></div>
<h3>Explanation:</h3>
<p>Ed Sheeran's song appeared twice in the Top 10 list of global song rank while Drake's song is only listed once. Therefore, Ed is ranked #1 and Drake is ranked #2.</p>
<p>The dataset you are querying against may have different input &amp; output - <strong>this is just an example</strong>!</p>

---

## My Notes

- You need to think backward and step by step

1. He wants top 10 global song rank
    - He doesn't care about if it was the top in the 1st day or the last one
2. He wants the singers of these songs
3. out of these singers give me the top 5
    - It might be a draw, if there is a one give me those as equal rank
4. you could learn about `DENSE_RANK()` [this article](https://www.sqlshack.com/overview-of-sql-rank-functions/) is useful for all rank functions

---

## Solutions

<details>
<summary> Solution </summary>
read the Notes first
you could learn about `DENSE_RANK()` [this article](https://www.sqlshack.com/overview-of-sql-rank-functions/) is useful for all rank functions

```sql
-- top 10 global songs
with top_10_by_id as (
    SELECT
        s.song_id song_id,
        COUNT(1) occ
    from
        global_song_rank gsr
        JOIN songs s on s.song_id = gsr.song_id
    WHERE
        rank <= 10
    GROUP BY
        s.song_id
),
-- merged these songs with `songs` table so i can get artist_id which i will use later
top_10 as (
    SELECT
        s.song_id,
        artist_id,
        occ
    FROM
        songs s
        JOIN top_10_by_id t on s.song_id = t.song_id
),
-- there might be songs share the same artist, so we need to sum the occurrence of artist songs
top_artist_with_occurrence as (
    SELECT
        artist_id,
        SUM(occ) occurrence
    FROM
        top_10
    GROUP BY
        artist_id
),
-- rank each artist by the number of occurrence in desc order
top_artist_with_rank as (
    select
        artist_name,
        DENSE_RANK() OVER(
            ORDER BY
                occurrence DESC
        ) artist_rank
    from
        top_artist_with_occurrence t
        join artists a on t.artist_id = a.artist_id
)
-- We want the top 5
SELECT
    artist_name,
    artist_rank
from
    top_artist_with_rank
WHERE
    artist_rank <= 5 

```

</details>

<details>
<summary> Solution </summary>
website solution

read the Notes first
you could learn about `DENSE_RANK()` [this article](https://www.sqlshack.com/overview-of-sql-rank-functions/) is useful for all rank functions

```sql
WITH top_10_cte AS (
    SELECT
        artists.artist_name,
        DENSE_RANK() OVER (
            ORDER BY
                COUNT(songs.song_id) DESC
        ) AS artist_rank
    FROM
        artists
        INNER JOIN songs ON artists.artist_id = songs.artist_id
        INNER JOIN global_song_rank AS ranking ON songs.song_id = ranking.song_id
    WHERE
        ranking.rank <= 10
    GROUP BY
        artists.artist_name
)
SELECT
    artist_name,
    artist_rank
FROM
    top_10_cte
WHERE
    artist_rank <= 5;

```

</details>

---

## Let's connect

I am Youssef Mohamed

- Linkedin: <https://www.linkedin.com/in/YoussefMo7amed>
- Github: <https://github.com/YoussefMo7amed>
