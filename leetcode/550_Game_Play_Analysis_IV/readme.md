```
Table: Activity

+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |
+--------------+---------+
(player_id, event_date) is the primary key (combination of columns with unique values) of this table.
This table shows the activity of players of some games.
Each row is a record of a player who logged in and played a number of games (possibly 0) before logging out on someday using some device.
 

Write a solution to report the fraction of players that logged in again on the day after the day they first logged in, rounded to 2 decimal places. In other words, you need to count the number of players that logged in for at least two consecutive days starting from their first login date, then divide that number by the total number of players.

The result format is in the following example.

 

Example 1:

Input: 
Activity table:
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |
+-----------+-----------+------------+--------------+
Output: 
+-----------+
| fraction  |
+-----------+
| 0.33      |
+-----------+
Explanation: 
Only the player with id 1 logged back in after the first day he had logged in so the answer is 1/3 = 0.33
```

# Solution
```
select 
    round(count(L.player_id) / player.cnt, 2) fraction
    
from activity a
left join (select player_id
                , min(event_date) first_login_date 
            from activity 
            group by player_id) L
    on (a.player_id = L.player_id
        and a.event_date = L.first_login_date+1)
    , (select count(distinct player_id) cnt from activity) player 
group by player.cnt
```

# Reflection
이 문제의 핵심은 각 플레이어의 `최초로그인일자(first_login_date)` 기준으로

다음 날 접속일자가 있는지 체크하는 것인데

나는 무조건 이틀 연속 로그인 한 플레이어 기준으로 했었다.

이 부분만 잘 인지했으면 30분은 절약했을 것 같다.
