# Critique: Word Count in Drafts

## What's strong
The two-step cleaning approach (LOWER + REGEXP_REPLACE before UNNEST) is the right instinct and worth highlighting as the core lesson.

## Coaching notes

1. **Hook** — "a word can explain many things" is too broad. Agreed to use the specific + unexpected angle: "I ran this on a set of drafts. The top word wasn't a product name or a client name. It was 'not'." Personal story with a specific detail drives LinkedIn reach.

2. **Logic** — original breakdown explains *what* each step does, not *why* the order matters. Key insight: cleaning before splitting is intentional — REGEXP_REPLACE on a raw string is predictable; cleaning after UNNEST risks missing tokens where punctuation is attached without a space boundary.

3. **Insight** — wordcloud mention is good but needs a business consequence frame, not just "can be used for wordcloud". What decision does word frequency enable?

4. **Takeaway** — "string processing needs these steps" is a topic heading. The rule is: clean before you split, because splitting depends on whitespace not word boundaries.

## Hook direction chosen
Specific + unexpected (option 3): personal story → insight → SQL structure.
