# Assignment 1 - Titanic Data Challenges (Warmup)

## Goal

Before you can visualize data you need to be comfortable pulling values out of it. This warmup uses the Titanic passenger dataset to practice counting, filtering, and deriving values with JavaScript — no drawing or DOM work yet.

## What to do

Complete the challenges in the Titanic Data Challenges repo:

https://github.com/Tech-at-DU/titanic-data-challenges

Fork or clone the repo, follow its instructions, and work through the challenges at your own pace. See [lesson-01](../lessons/lesson-01.md) and [lesson-02](../lessons/lesson-02.md) for background on arrow functions, callbacks, `map`/`filter`/`reduce`, and building histograms — all of which come up in these challenges.

## Learning Objectives

- Identify values in the Titanic dataset
- Extract data and derive relevant values (counts, min, max, averages)
- Use `map`, `filter`, and `reduce` to work with an array of objects

## What will you turn in?

Post a link to your GitHub repo containing your solutions to GradeScope (or wherever your program collects submissions).

## Evaluating your work

| Aspect | Does not meet | Meets | Exceeds |
|:-------|:--------------|:------|:--------|
| **Completion** | Fewer than half of the challenges are solved | Most challenges are solved correctly | All challenges are solved correctly |
| **Code style** | Inconsistent style, poorly named variables | Consistently styled, self-documenting, follows best practice | Code reviewed by a peer |

### Learning Objectives Rubric

| Aspect | Does not meet | Meets | Exceeds |
|:-------|:--------------|:------|:--------|
| **Identify Values in Titanic Dataset** | Can't identify values in the dataset | Can identify values in the dataset | Feels confident identifying values in any dataset |
| **Extracting Data** | Can't extract or derive values from the dataset | Can extract relevant values from the dataset | Could extract values from any dataset |
| **Deriving Values** | Can't derive count, min, and max values | Can derive count, min, and max values | Could derive range, average, and other aggregate values |

## Optional practice: display what you found

Once you're comfortable extracting values, try displaying a few of them as HTML elements generated with JavaScript — no charting library, just `document.createElement` and inline styles. [lesson-04](../lessons/lesson-04.md) walks through exactly this using the Titanic data (create a `<div>` per passenger, style it based on `survived`, `sex`, or `pclass`). This isn't a required deliverable — it's a good stepping stone toward Assignment 2.
