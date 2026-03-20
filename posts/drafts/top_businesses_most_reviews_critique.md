# Coaching Critique — top_businesses_most_reviews

## What's Strong
The SQL logic is correct: CTE with aggregation, then filter on rank. Choosing RANK() over ROW_NUMBER() is the right call. The problem link is included.

## Coaching Notes

1. **Hook: no failure angle.**
   The draft opens with the solution. The real hook is the silent failure: if you use ROW_NUMBER() on a tied leaderboard, one of the top businesses gets arbitrarily dropped and nobody notices. Start from that scenario, not from "here's the answer."

2. **Logic: "skips counting" is backwards.**
   RANK() skips rank *numbers* after a tie (two businesses tied at rank 3 means the next rank is 5, not 4). That is not why it is correct here. The correct reason: RANK() keeps all tied businesses within the top-5 cutoff. ROW_NUMBER() arbitrarily excludes one. Explain the *consequence of the wrong choice*, not just the mechanism.

3. **Logic: unnecessary ORDER BY inside the CTE.**
   `ORDER BY 3 desc` inside a CTE has no guaranteed effect — the window function handles ranking. Drop it to avoid misleading readers.

4. **Insight: "sometime its predetermined" is ungrounded.**
   The insight needs a real business scenario: a Yelp "Top 5" report where two businesses have identical review counts. Which ones appear? All of them, or only one? That consequence makes the insight land.

5. **Takeaway: "remember which one is correct" is a topic heading.**
   Push toward a decision rule: "When [condition], use [X] because [consequence of not doing so]." Example: "When the top-N cutoff has ties, use RANK() — ROW_NUMBER() silently drops tied entries and corrupts the leaderboard."
