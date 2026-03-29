---
draft: best_selling_item_raw.md
language: Indonesian (mixed with English SQL)
---

# Critique — Best Selling Item

**Yang kuat:** SQL-nya bersih dan benar. Business framing-nya kaya. Takeaway terakhir (unit vs revenue) punya bite nyata — itu adalah satu-satunya bagian dari draft ini yang menghasilkan sebuah rule yang bisa dipakai.

---

## Coaching notes

1. **Hook masih kosong — dan takeaway-mu sendiri adalah jawabannya.**
   Kamu bilang "best selling item bisa dilihat bukan hanya dari total paid tapi juga dari jumlah item terjual." Itu adalah failure scenario-nya: kamu bisa menjalankan query ini dengan sempurna dan masih menjawab pertanyaan yang salah, tergantung definisi "best."
   Hook yang dipilih (Angle 1): *"Before I wrote a single line of SQL, my manager and I had to agree on what 'best-selling' actually means."*

2. **`WHERE quantity > 0` tidak dijelaskan, tapi ini adalah pilihan paling penting di seluruh query.**
   Dataset online_retail menyimpan returns sebagai quantity negatif. Kalau filter ini tidak ada, item yang paling banyak di-return bisa muncul sebagai "best seller" karena magnitude revenue-nya tinggi. Silent wrong result — query jalan, output terlihat masuk akal.

3. **Business insight terlalu lebar — tiga arah sekaligus.**
   Recommendation engine, push similar items, pricing/discount strategy. Angle yang paling tajam dan langsung actionable dari output query ini: kalau kamu memberikan diskon di bulan di mana item itu sudah jadi best seller, kamu membuang margin. Peak-season items tidak butuh diskon untuk laku.

4. **Takeaway adalah insight, bukan rule.**
   "Best selling bisa dilihat dari total paid atau jumlah terjual" adalah topik. Rule-nya: *"Tentukan definisi 'best' sebelum menulis query — revenue dan units bisa menghasilkan pemenang yang berbeda, dan kedua hasilnya terlihat benar."*

---

Hook dipilih: **Angle 1** (define the metric before writing the query).
