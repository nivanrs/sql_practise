WITH Olymp AS (
  SELECT games, COUNT(DISTINCT id) AS athletes
  FROM olympics_athletes_events
  GROUP BY games
)
SELECT *
FROM Olymp
WHERE athletes = (
  SELECT MAX(athletes)
  FROM Olymp
);


problems: https://platform.stratascratch.com/coding/9942-largest-olympics

logic: buat grouping per games dan hitung discting id nya, karena bisa satu orang yang sama ada di berbagai cabang yang berbeda, setelah itu buat conditional dimana jumlah atlit dalah count terbanyaknya

kenapa tidak make ini:
select games, count(distinct id) from olympics_athletes_events
group by games
order by 2 desc
limit 1

secara teknis ini benar namun jika hanya melimit 1 hasil saja, ada potensi untuk menghilangkan jawaban olimiade terbanyak yang memiliki atlet yang sama

Pettern ini memberitahukan bahwa: kalaupun benar maka bisa saja kebenaran itu mengandung potensi kesalahan di kemudian hari

key takeways: selalu cek hasil dan liat tabel yang dihasilkan
