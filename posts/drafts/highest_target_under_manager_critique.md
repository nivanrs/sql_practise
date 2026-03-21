# Coaching Critique: Highest Target Under Manager

## Draft Notes
- Language: SQL + commentary
- No hook, no prose, no business framing
- "nothing new here, its just usual rank and filtering" signals the author knows the pattern is thin

## Hook
**Missing.** No failure scenario. The reader has no reason to care. "Nothing new here" is the intro equivalent of a shrug. What goes wrong when this pattern is written wrong? If the query returned two employees with the same target, the naive version (no subquery, just ORDER BY DESC LIMIT 1) would silently drop one. That is the hook.

## Logic
**Too brief to evaluate properly.** No breakdown of what the subquery does vs. the outer query. The `1=1` is a SQL artifact with no logical meaning here — worth noting. No explanation of why LIMIT 1 is safe inside the subquery (it finds the target value, not the row). The "rank and filtering" reference is vague.

## Insight
**Absent.** What does this query actually answer in business terms? Who cares about a manager's highest-target employee? Performance review? Compensation planning? Commission alerts? The query is described as mechanical, not consequential.

## Takeaway
**Missing.** The commentary doesn't lift into a reusable rule. What should the reader learn from this? "Use a subquery to isolate the target value before filtering" is not a takeaway — it's a description of the code.

## Readiness Check
Not ready. The draft is a brain dump with no structural intent. Coaching required before writing.
