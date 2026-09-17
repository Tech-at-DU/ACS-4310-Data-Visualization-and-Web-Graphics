
# ACS 4310 - Project Kickoff: Build Visualization 1

## Lab

By the end of today you should have: your three questions written down, the fields from your dataset that answer them identified, real data loaded and shaped in code, and a blank SVG sized with a margin convention. That's the skeleton every chart in [Assignment 2](../Assignments/assignment-2.md) is built on.

<!-- > -->

## Overview

- Lock in the three questions your first visualization will answer
- Identify which fields in your dataset those questions need
- Extract and arrange (sort/filter/aggregate) just that subset
- Set up size, margins, scales, and axes — the skeleton of every D3 chart

<!-- > -->

## Why you should know this

Picking a chart type is the easy part — [data-to-viz.com](https://www.data-to-viz.com) and [datavizproject.com](https://datavizproject.com) do that for you. The harder, more valuable skill is going from "here's a chart type" to "here's working code against my real data." That means shaping data into the exact structure a chart needs, and setting up the size/margin/scale/axis scaffolding every D3 chart shares. Get this skeleton right once and you'll reuse it for all three of your visualizations.

<!-- > -->

## Learning Objectives

1. State three questions a visualization will answer, and name the dataset fields each question needs
1. Extract and arrange (sort/filter/aggregate) a subset of a dataset with code
1. Set up an SVG with the margin convention (width, height, margins)
1. Define scales (domain → range) and render axes from real data

<!-- > -->

## Warm-up: Your three questions (5 min, solo)

Assignment 2 asks you to ask three questions of each dataset. Today you're only building **Visualization 1** — so write down, in one line each:

1. Question 1:
1. Question 2:
1. Question 3:

Keep these next to you. Everything else today serves these three lines.

**Example — Titanic passenger dataset:**

1. How many passengers lived and how many died, by gender?
1. How many passengers lived and died, by passenger class?
1. Did having a sibling aboard affect your chance of survival?

Notice each one names a comparison (lived vs. died) *and* a category to break it down by (gender, class, siblings). A good question almost always has both parts — if yours only has one, it's not specific enough yet.

<!-- > -->

## Turn questions into fields (10 min, pairs)

Trade questions with a partner. For each question, answer:

- Which **field(s)** in your dataset does this question need?
- Is each field **categorical** (axis groups, color) or **numeric** (position, length, size)?
- Does answering it require the *raw* rows, or a **derived** value — a count, sum, or average grouped by category?

If you can't point to a field, the question is too vague — rewrite it now, before you write any code.

**Example — Titanic, question 1** ("lived and died, by gender?"):

| | |
|---|---|
| Fields needed | `survived`, `sex` |
| `sex` | categorical → x-axis groups |
| `survived` | categorical (0/1) → but you'll **derive** a count from it |
| Raw or derived? | Derived — count of passengers, grouped by `sex` and `survived` |

<!-- > -->

## Extract and arrange your data (20 min, code)

Most datasets aren't shaped the way a chart needs them. Load your data, then write the code that gets you from "raw rows" to "exactly what my chart draws."

Common shapes you'll need:

```js
// Filter: keep only the rows relevant to your question
const subset = data.filter(d => d.pclass === "3rd")

// Sort: order matters for bar charts, line charts, rankings
const sorted = [...data].sort((a, b) => b.age - a.age)

// Group + aggregate: turn many rows into one summary value per category
const grouped = d3.groups(data, d => d.sex)
const summarized = grouped.map(([key, rows]) => ({
  sex: key,
  survived: d3.sum(rows, d => d.survived === "1" ? 1 : 0)
}))
// -> [{ sex: "male", survived: 109 }, { sex: "female", survived: 233 }]
```

That last shape is exactly what answers Titanic question 1 — survival count, grouped by gender.

**Checkpoint:** `console.log` the exact array your chart will consume. If you can't describe its shape in one sentence ("an array of objects with `category` and `total`"), keep working before moving on.

<!-- > -->

## Set up size and margins (10 min, code)

Every D3 chart starts the same way. Use the margin convention so axes and labels have room outside the plot area:

```js
const margin = { top: 20, right: 20, bottom: 40, left: 60 }
const width = 600 - margin.left - margin.right
const height = 400 - margin.top - margin.bottom

const svg = d3.select("#chart")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", `translate(${margin.left}, ${margin.top})`)
```

Everything you draw next goes inside that inner `g` — position `0,0` is the top-left of your *plot area*, not the SVG.

<!-- > -->

## Define scales and axes (20 min, code)

Scales map your data's domain onto pixel space. Pick scales based on the field types you identified earlier:

| Scale | Domain (data) | Use for |
|---|---|---|
| `d3.scaleLinear` | continuous number | numeric field → position, length, radius (age, fare, survived count) |
| `d3.scaleBand` | discrete categories | categorical field → grouped position on an axis (sex, pclass, embarked) |
| `d3.scaleOrdinal` | discrete categories | categorical field → non-position visual, usually color |
| `d3.scaleTime` | dates | a date/time field → position on a time axis |
| `d3.scaleSqrt` / `d3.scalePow` | continuous number | numeric field → **area** encodings (circle radius), so the *area* scales correctly instead of the radius |
| `d3.scaleLog` | continuous number | numeric field with a huge range/skew (a few outliers dwarf everything else) |

Rule of thumb: categorical field → `scaleBand` (position) or `scaleOrdinal` (color). Numeric field → `scaleLinear`, unless it's a date (`scaleTime`), it's driving a circle's radius (`scaleSqrt`), or it's wildly skewed (`scaleLog`).

```js
// Numeric (derived) field → position/length
const y = d3.scaleLinear()
  .domain([0, d3.max(summarized, d => d.survived)])
  .range([height, 0])

// Categorical field → grouped position
const x = d3.scaleBand()
  .domain(summarized.map(d => d.sex))
  .range([0, width])
  .padding(0.2)

svg.append("g")
  .attr("transform", `translate(0, ${height})`)
  .call(d3.axisBottom(x))

svg.append("g")
  .call(d3.axisLeft(y))
```

**Checkpoint:** you should see two axes on screen, drawn from *your* data, before you draw a single bar/line/point.

<!-- > -->

## Lab: put it together

Working from your own dataset and three questions:

1. Extract/arrange the subset for **Question 1** only
1. Set up size + margins
1. Define scales from that subset's domain
1. Render both axes

Don't draw the marks (bars, dots, lines) yet. Your first goal is a correctly-scaled, correctly-labeled empty chart.

<!-- > -->

## After this lesson

- Keep this size/margin/scale/axis setup — you'll copy and adapt it for all three visualizations
- Move on to [lesson-13](./lesson-13.md) if a map fits one of your datasets
- Otherwise, next class: drawing marks from your scaled data

<!-- > -->

## Additional Resources

- https://www.data-to-viz.com
- https://datavizproject.com
- https://d3indepth.com/scales/
- https://d3indepth.com/axes/
- https://github.com/soggybag/d3-examples
- https://github.com/soggybag/FEW-2-5-Data-Visualization-D3

<!-- > -->

<!--
## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**                          |
| ----------- | --------- | -------------------------------------- |
| 0:00        | 0:05      | Overview + Learning Outcomes           |
| 0:05        | 0:05      | Warm-up: write your three questions    |
| 0:10        | 0:10      | Pairs: turn questions into fields      |
| 0:20        | 0:20      | Extract and arrange data (code)        |
| 0:40        | 0:10      | Size and margins (code)                |
| 0:50        | 0:20      | Scales and axes (code)                 |
| 1:10        | 0:10      | Break                                  |
| 1:20        | 1:15      | Lab: build your own skeleton chart     |
| 2:35        | 0:05      | Wrap up                                |
| TOTAL       | 2:45      | -                                       |
-->
