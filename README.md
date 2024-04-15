# sql-query-solving-
solving sql queries -project
- # [stratascratch-9791-highest view count first](https://platform.stratascratch.com/coding/9791-views-per-keyword?code_type=3))



### Create a report showing how many views each keyword has. Output the keyword and the total views, and order records with highest view count first.

```
select facebook_posts.post_keywords ,
facebook_post_views.viewer_id as total_viewcount
from facebook_posts
left join facebook_post_views on facebook_posts.post_id =facebook_post_views.	post_id
group by facebook_posts.post_id
order by facebook_post_views.viewer_id desc
;
```
- # [https://platform.stratascratch.com/coding/9979-find-the-top-5-highest-paid-and-top-5-least-paid-employees-in-2012?code_type=3](https://svrsudheer.github.io/sql-query-solving-/)
```
SELECT 
     employeename, totalpaybenefits
     from
    
    (SELECT 
         employeename, totalpaybenefits,
         dense_rank() over(order by totalpaybenefits asc) as salary_rank
         
     FROM
         sf_public_salaries
     WHERE year = 2012
     ORDER BY salary_rank asc limit 5) AS t1
     union
     SELECT 
     employeename, totalpaybenefits
     from
    
    (SELECT 
         employeename, totalpaybenefits,
         dense_rank() over(order by totalpaybenefits asc) as salary_rank
         
     FROM
         sf_public_salaries
     WHERE year = 2012
     ORDER BY salary_rank desc limit 5) AS t2
     
     
     order by totalpaybenefits asc
   ;
```
