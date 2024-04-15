# sql-query-solving-
solving sql queries -project
# [https://platform.stratascratch.com/coding/9791-views-per-keyword?code_type=3](https://svrsudheer.github.io/sql-query-solving-/)



### Create a report showing how many views each keyword has. Output the keyword and the total views, and order records with highest view count first.


`select facebook_posts.post_keywords ,
facebook_post_views.viewer_id as total_viewcount
from facebook_posts
left join facebook_post_views on facebook_posts.post_id =facebook_post_views.	post_id
group by facebook_posts.post_id
order by facebook_post_views.viewer_id desc
;`
