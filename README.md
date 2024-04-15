# sql-query-solving-
solving sql queries -project
- # [stratascratch-9791-highest view count first-(https://platform.stratascratch.com/coding/9791-views-per-keyword?code_type=3)](https://platform.stratascratch.com/coding/9791-views-per-keyword?code_type=3)



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
- # [https://platform.stratascratch.com/coding/9979-find-the-top-5-highest-paid-and-top-5-least-paid-employees-in-2012?code_type=3](https://platform.stratascratch.com/coding/9979-find-the-top-5-highest-paid-and-top-5-least-paid-employees-in-2012?code_type=3)
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
- # [https://platform.stratascratch.com/coding/10131-business-name-lengths?code_type=3](https://platform.stratascratch.com/coding/10131-business-name-lengths?code_type=3)

```
select business_name,
        regexp_replace(business_name,'[&,#]' ,''),
        length(regexp_replace(business_name,'[&,#]' ,''))
             from 
             sf_restaurant_health_violations;
```
- # [https://platform.stratascratch.com/coding/10172-best-selling-item?code_type=3](https://platform.stratascratch.com/coding/10172-best-selling-item?code_type=3)

```
select description, max(unitprice*quantity) from online_retail
group by month(invoicedate)

;

select description, month(invoicedate),max(unitprice*quantity) from online_retail
group by month(invoicedate)
order by 2
```
- # [https://platform.stratascratch.com/coding/2038-wfm-brand-segmentation-based-on-customer-activity?code_type=3](https://platform.stratascratch.com/coding/2038-wfm-brand-segmentation-based-on-customer-activity?code_type=3)


note----problem when using case statement 
```
select  wfm_stores.store_brand
,count(wfm_transactions.customer_id) as number_of_customers
,count(wfm_transactions.transaction_id) as number_of_transactions 
,sum(wfm_transactions.sales) as total_sales,
sum(wfm_transactions.sales)/count(wfm_transactions.transaction_id) as avgsale,
case(sum(wfm_transactions.sales)/count(wfm_transactions.transaction_id)) 
when (sum(wfm_transactions.sales)/count(wfm_transactions.transaction_id)) > 30 then 'high'
when (sum(wfm_transactions.sales)/count(wfm_transactions.transaction_id)) between 20 and 30 then 'medium'
else 'low'
end as segment

from wfm_transactions
join wfm_stores on wfm_stores.store_id=wfm_transactions.store_id
where year(wfm_transactions.transaction_date) = 2017
group by wfm_stores.store_brand,wfm_transactions.customer_id
;
```
- # Most Profitable Companies
- # [https://platform.stratascratch.com/coding/10354-most-profitable-companies?code_type=3](https://platform.stratascratch.com/coding/10354-most-profitable-companies?code_type=3)
select company, MAX(profits) AS most_profitable
from forbes_global_2010_2014
GROUP BY company
ORDER BY most_profitable DESC
LIMIT 3;
