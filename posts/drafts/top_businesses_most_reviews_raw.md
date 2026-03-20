with business_rank as(
select business_id, name, sum(review_count) review_count, rank() over (Order by sum(review_count) desc) as rank

from yelp_business

group by business_id, name
order by 3 desc
)

select name, review_count from business_rank
where rank <= 5

from problem:https://platform.stratascratch.com/coding/10048-top-businesses-with-most-reviews?code_type=1

logic: this problem is related to applied correct rank, the most correct is rank() because its skips counting

this pattern tells you: remember the rule and business context, sometime its predetermined

key takeways: remember which one is correct windows function
