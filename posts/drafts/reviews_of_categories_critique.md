# Critique: reviews_of_categories

## What's strong
SQL is clean and correct. `unnest(string_to_array(...))` is the right tool and the CTE structure reads clearly.

---

## Coaching Notes

### 1. Hook: tidak ada failure scenario
Draft langsung lompat ke solusi. Tidak ada momen "apa yang salah kalau pakai pendekatan yang salah?"
- Kalau pakai `SPLIT_PART` dengan index tetap, kamu hanya dapat satu kategori per baris, bukan semua.
- Kalau `GROUP BY categories` tanpa split, setiap kombinasi dianggap berbeda ("Restaurants;Bars" ≠ "Bars;Restaurants").
Mulai dari failure scenario itu.

### 2. Logic: penjelasan `unnest` kurang tepat
> "dalam postgree string split harus mendeklarasikan berapa n nya"

Ini tidak akurat. `SPLIT_PART` butuh index `n`, tapi itu bukan alasan pakai `unnest`. Kita pakai `unnest` karena ia meng-expand satu array menjadi multiple rows. `string_to_array` menghasilkan array; `unnest` yang meledakkannya jadi baris. Dua fungsi berbeda, perlu dijelaskan perannya masing-masing.

### 3. Insight: "view baru dari agregasi" terlalu abstrak
Contoh konkret lebih kuat: "Kamu bisa tahu bahwa 'Restaurants' punya total 2.1 juta review, padahal tidak ada satu baris pun yang labelnya cuma 'Restaurants'." Itu kejutan yang layak ditekankan.

### 4. Takeaway: "perlu perlakuan khusus" terlalu samar
"Perlu perlakuan khusus" adalah topik, bukan pelajaran. Lebih tajam: "Kalau data tersimpan sebagai delimited string atau JSON array, kamu butuh expand dulu sebelum aggregate, karena GROUP BY tidak bisa membaca di dalam string."

---

## Status
Awaiting user confirmation before writing final post.
