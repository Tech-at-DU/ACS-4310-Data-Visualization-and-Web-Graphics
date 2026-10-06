
# ACS 4310 - Pick Your Upgrade

## Overview

Four small, independent D3 upgrades: **tooltips**, **number formatting**, **transitions**, and **legends**. Each is its own short mini-tutorial — pick the one that's most useful for whatever visualization you're currently building, work through it, and drop it into your code today. You don't need all four; pick one now, come back for the others later.

<!-- > -->

## Why you should know this

These are small, but they're the difference between a chart that just displays data and one that reads as finished — "exceeds" territory on the rubric instead of "meets." Each one is also something you'll reach for constantly outside this class.

<!-- > -->

## Learning Objectives

Pick the objective that matches the option you choose:

1. Show a value on hover with a tooltip
1. Format raw numbers into readable labels with `d3.format()`
1. Animate marks entering/updating with `.transition()`
1. Build a small color legend next to a chart

<!-- > -->

## How to use this lesson

Each section below is self-contained and generic — written against placeholder names (`svg`, `marks`, `x`, `y`, `color`) so you can drop it into whatever chart you're already building, regardless of chart type. Pick one, build it, test it on your own data. If you finish early, come back and pick another.

<!-- > -->

## Option A: Tooltips on hover

Show a value when the mouse is over a mark — one of the highest-payoff upgrades for the least code.

**Pattern:**

```js
// Once, outside your draw code: a hidden div positioned absolutely
const tooltip = d3.select("body")
  .append("div")
    .style("position", "absolute")
    .style("background", "white")
    .style("border", "1px solid #333")
    .style("padding", "4px 8px")
    .style("pointer-events", "none")
    .style("opacity", 0)

// On your existing marks (bars, circles, whatever you already drew):
marks
  .on("mouseover", (event, d) => {
    tooltip.style("opacity", 1)
  })
  .on("mousemove", (event, d) => {
    tooltip
      .html(`${d.category}: ${d.value}`)   // whatever fields you have
      .style("left", (event.pageX + 10) + "px")
      .style("top", (event.pageY - 20) + "px")
  })
  .on("mouseout", () => {
    tooltip.style("opacity", 0)
  })
```

`event` is the native mouse event, `d` is the datum bound to the mark you're hovering — same `d` you already use when drawing it.

**Try it:** add this to whatever marks you've already drawn, swap `d.category`/`d.value` for your real fields.

<!-- > -->

## Option B: Readable numbers with `d3.format()`

Raw numbers are often ugly on an axis or in a tooltip — too many decimals, no thousands separator. `d3.format()` takes a tiny spec string and returns a formatting function.

```js
const formatCount = d3.format(",")        // 12000 -> "12,000"
const formatPercent = d3.format(".0%")    // 0.4231 -> "42%"
const formatMoney = d3.format("$,.2f")    // 1234.5 -> "$1,234.50"

// Use it on an axis:
svg.append("g").call(d3.axisLeft(y).tickFormat(formatCount))

// Or in a tooltip/label:
tooltip.html(`${d.category}: ${formatCount(d.value)}`)
```

**Try it:** pick whichever spec matches your value (plain count, percent, or currency) and apply it to one of your existing axes.

<!-- > -->

## Option C: Transitions

Animate marks when they first appear, or when their values change — makes a chart feel alive instead of just appearing instantly.

```js
svg.selectAll(".bar")
  .data(data)
  .join("rect")
    .attr("class", "bar")
    .attr("x", d => x(d.category))
    .attr("width", x.bandwidth())
    .attr("y", height)        // start flat, at the bottom
    .attr("height", 0)
  .transition()                // everything after this animates
    .duration(750)
    .attr("y", d => y(d.value))
    .attr("height", d => height - y(d.value))
```

The trick: set the **starting** attributes first (outside `.transition()`), then chain `.transition().duration(ms)` and set the **ending** attributes — D3 animates between the two automatically.

**Try it:** apply this to however you're currently drawing bars/circles/lines — set a "start" state, then transition to the real one.

<!-- > -->

## Option D: Legend

A small, reusable block that shows what each color means — pairs with any chart using `d3.scaleOrdinal()` for color.

```js
const legend = svg.append("g")
  .attr("transform", `translate(${width - 100}, 10)`)

const entries = legend.selectAll("g")
  .data(color.domain())   // the categories your color scale knows about
  .join("g")
    .attr("transform", (d, i) => `translate(0, ${i * 20})`)

entries.append("rect")
  .attr("width", 12)
  .attr("height", 12)
  .attr("fill", color)

entries.append("text")
  .attr("x", 18)
  .attr("y", 10)
  .text(d => d)
```

`color.domain()` reuses the same categories you already passed into your `scaleOrdinal` — no need to hardcode them a second time.

**Try it:** if any of your charts use color to encode a category, add this next to it.

<!-- > -->

## Lab

Pick **one** option above and add it to whichever visualization you're actively building. Commit it before moving on. If you have time left, pick a second.

**Checkpoint:** show a partner your upgrade working on real data, not placeholder values.

<!-- > -->

## After this lesson

Keep working on your [three visualizations](../Assignments/assignment-2.md) — [lesson-16](./lesson-16.md) (wrap-up and review) is next, ahead of the final assessment. Come back to the options you didn't pick whenever a chart could use them.

## Additional Resources

**Tooltips**

- https://d3-graph-gallery.com/graph/interactivity_tooltip.html

**Formatting**

- https://d3js.org/d3-format
- https://github.com/d3/d3-format

**Transitions**

- https://d3indepth.com/transitions/

**Legends**

- https://d3-graph-gallery.com/graph/custom_legend.html
- https://d3-legend.susielu.com/

<!-- > -->
