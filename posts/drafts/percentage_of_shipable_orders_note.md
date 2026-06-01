# Percentage of Shipable Orders note

Rescheduled as part of the post backlog after stopping publication after 2026-04-13.

New planned posting date: 2026-06-01

## Content direction

This post should frame shippability as an operations and fulfillment check, not only a SQL percentage problem.

The useful business angle: orders with missing customer addresses look valid in the order table, but they cannot be fulfilled. If the team does not measure this rate, fulfillment teams discover the issue too late, after planning capacity, stock movement, or dispatch work.

## Hook angle

A paid order is not always a shippable order.

That line creates the failure scenario before the SQL appears.

## Technical lesson

Use `AVG((condition)::INT) * 100` when each row needs to contribute either 1 or 0 to a percentage.

This is cleaner than writing two separate aggregate expressions when the denominator is all joined order rows and the numerator is rows where the condition is true.

## LinkedIn first comment

Post the StrataScratch link as the first comment:

https://platform.stratascratch.com/coding/10090-find-the-percentage-of-shipable-orders?code_type=1
