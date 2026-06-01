## 💻 SQL of the Day: Word Count in Drafts
🔗 https://platform.stratascratch.com/coding/9817-find-the-number-of-times-each-word-appears-in-drafts?code_type=1 — StrataScratch #9817

### Problem:
Find the number of times each word appears across all drafts stored in google_file_store. Output each word and its count, ordered by frequency descending.

---

### 🧠 SQL Solution
```sql
with raw as (
    select
        LOWER(REGEXP_REPLACE(word, '[^a-zA-Z0-9]', '', 'g')) AS word
    from google_file_store,
    UNNEST(STRING_TO_ARRAY(contents, ' ')) AS word
)

select word, count(*) as occurrences
from raw
group by word
order by 2 desc
```

---

### 🧩 Simple logic breakdown
- `STRING_TO_ARRAY(contents, ' ')` splits each document's text into an array of tokens, splitting on spaces.
- `UNNEST(...)` explodes that array so each token becomes its own row — one row per word per document.
- `REGEXP_REPLACE(word, '[^a-zA-Z0-9]', '', 'g')` strips every non-alphanumeric character from each token. This removes trailing periods, commas, and quotes that would otherwise make `"word."` and `"word"` count as separate entries.
- `LOWER(...)` normalizes case so `"Draft"`, `"draft"`, and `"DRAFT"` collapse into one.
- Cleaning happens before grouping because the raw token still holds its punctuation at this stage. If you skipped this step, your frequency table would silently fragment every word that appears at a sentence boundary.
- `COUNT(*)` then aggregates across the cleaned tokens.

---

### 📊 This pattern tells you
- Which words dominate a document corpus, revealing the actual vocabulary of a team or process rather than the intended one.
- Where sentiment lives without a sentiment model: a corpus where "not", "issue", or "blocked" ranks in the top 10 is telling you something before any ML model touches the data.
- A baseline for document health checks: drafts heavy with hedge words ("maybe", "consider", "pending") signal unresolved decisions, not finished work.
- The same query feeds a wordcloud directly. Feed the output to any visualization library and the frequency distribution becomes immediately readable.

---

### 🎯 Key takeaways
1. Clean before you split. `REGEXP_REPLACE` on a full string is predictable. Cleaning after `UNNEST` means you are operating on fragments, and tokens where punctuation runs directly into the next word (no space) will survive the split uncleaned.
2. `LOWER()` and `REGEXP_REPLACE` together are the minimum viable normalization for any word frequency task. Either one alone still produces fragmented counts.
3. Word frequency is a proxy for attention. What people write most is what they are actually thinking about, regardless of what the document is supposed to cover.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #TextAnalytics #StringProcessing #NLP
