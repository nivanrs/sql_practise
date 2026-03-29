with raw as (
select
EXTRACT(MONTH FROM invoicedate) as month,
description,
unitprice * quantity as total_paid


from online_retail
where quantity > 0
),

agg AS (
    SELECT
        month,
        description,
        SUM(total_paid) AS total_paid
    FROM raw
    GROUP BY month, description
),

ranked as (
select month, description, total_paid,
RANK() OVER (PARTITION BY month ORDER BY total_paid DESC) AS rank

from agg
)

select month, description, total_paid
from ranked
where rank = 1
;

logic: extract month from existing data, create noew column based on the current column, aggregate it so it has total, and the rank it

business impact: ada beberapa item yang hanya laku di bulan tertentu, pattern in bisa digunakan untuk merekomendaikan item ke orang yang belum pernah membelinya di bulan itu atau mempush item yang similar denagn item yang laku di bulan tersebut. Secara cost juga untuk item yang udah laku ga usah ada diskon yang berlebihan, tapi ini perlu dikaji lebih dalam apakan orang yang membelinya price sensitive atau tidak.

link problem ada di: https://platform.stratascratch.com/coding/10172-best-selling-item?code_type=1

key takeways: best selling item bisa dilihat bukan hanya dari total paid tapi juga dari jumlah item terjual juga

hook: ?
