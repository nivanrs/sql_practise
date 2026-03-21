## Coaching Critique — largest_olympics

### Strength
Strong pattern recognition: the draft correctly identifies that `LIMIT 1` silently drops ties, which is a real and subtle class of SQL bug.

---

### Hook
**Missing failure angle.** The draft starts from the solution, not from the problem. A reader who already believes `ORDER BY + LIMIT 1` is correct has no reason to pause.

The failure scenario to name: imagine two Olympics editions with the exact same number of distinct athletes. `LIMIT 1` returns one arbitrarily; the correct query returns both. If stakeholders act on the "winner," they may be acting on a coin flip.

---

### Logic
**Good.** The CTE approach is the correct pattern here.

One precision note on the draft text: the phrase "jumlah atlit dalah count terbanyaknya" has a typo ("dalah"). Fix it to "adalah".

---

### Insight
**Grounding needed.** "Kebenaran itu mengandung potensi kesalahan di kemudian hari" is philosophically true but too abstract for a LinkedIn audience scanning for usable takeaways.

Ground it in the Olympic scenario: if two editions tie for most athletes and you only show one, your "leaderboard" is wrong. This happens in real data — Olympics participation fluctuates, and ties are plausible.

---

### Takeaway
**Not yet a lesson.** "Selalu cek hasil dan liat tabel yang dihasilkan" is a topic heading, not a rule. Push toward the specific decision:

"When grouping and counting distinct entities, prefer conditional equality (`= (SELECT MAX(...))`) over `ORDER BY + LIMIT 1` — the latter silently discards ties, producing wrong results that look correct until edge cases appear."

---

### Ready to write the final post?
Yes, the raw material is solid. Fix the hook and takeaway before drafting the `.md`.
