problems: https://platform.stratascratch.com/coding/10049-reviews-of-categories?code_type=1

solutions:
with split_category as (

select
    unnest(string_to_array(categories, ';')) AS category,
    review_count
from yelp_business
)

select category, sum(review_count) no_of_reviews from split_category

group by 1
order by 2 desc
;

logic: pahami bentuk tabel seperti apa, di tabel ini kategori berupa string dengan pemisah, tentunya membutuhkan string split, tapi dalam postgree string split harus mendeklarasikan berapa n nya , sehingga yang cocok adalah unnest, setelah terpisah lalu di grouping

this pattern tells you: situasi seperti ini umum terjadi, beberapa entitas masuk ke dalam beberapa kategori, dengan menghitung jumlah per kategori kita bisa mendapat view baru dari agregasi tersebut

key takeway: column dengan multiple value itu umum, banyak juga yang masih dalam bentuk json sehinga perlu perlakuan khusus
