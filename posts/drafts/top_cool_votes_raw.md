# RAW DRAFT: Top Cool Votes

Source: https://platform.stratascratch.com/coding/10060-top-cool-votes?code_type=1

---

ini postingan sql of the day saya, improve

solusi:
with rank_list as (select business_name, review_text, cool, dense_rank() over (order by cool desc) as rank from yelp_reviews
order by 4
)
select business_name, review_text
from rank_list
where rank=1
;

logic: urutkan rank yang sesuai terus filter column mana yang mau diperlihatkan

this insight tells you: dalam rank yang paling adil adalah dengan menggunakan dense rank, sebab ini melihat mana yang memiliki hasil yang sama, tidak ada kejadian terfilter

key takeaway harus tau kapan pake dense rank, rank, dan row
