
# ACS 4310 - D3 Intro

## Overview

D3 is a library that has been around for a long time. It's more of a toolkit for making visualizations with JavaScript. It's the first name that comes when conversation turns to making data visualizations with JS.

## Why you should know this

It's the tool that wrote the book on data visualization with JS. You can do just about anything with D3. It has huge flexibility and deep toolset.

<!-- > -->

## Learning Objectives

- Identify use cases for D3
- Define data used by D3
- Create simple visualizations with D3

<!-- > -->

## D3

D3 - Data Driven Documents describes itself as:

> D3.js is a JavaScript library for manipulating documents based on data. D3 helps you bring data to life using HTML, SVG, and CSS. D3’s emphasis on web standards gives you the full capabilities of modern browsers without tying yourself to a proprietary framework, combining powerful visualization components and a data-driven approach to DOM manipulation.

What does it do? Data visualization! You could say D3 wrote the book on data visualization with JavaScript.

<!-- > -->

## How does it work?

D3 does so much it's hard to answer that. It draws things from data. It binds to data, meaning it will update when the data changes. It handles animation and interactions. It can load data and manipulate the DOM.

D3 is more of a toolbox with tools that are focussed on drawing things on the screen from a datasets.

<!-- > -->

## Explore D3.

Go to the [D3 hompage](https://d3js.org), and take a look at the examples on the D3 home and [examples pages](https://github.com/d3/d3/wiki/Gallery).

**Find an example that you think is interesting to show to the group and answer the question: _why is this interesting?_**

D3 is complex. With that complexity comes a lot of flexibility. Expect a steep learning curve!

<!-- > -->

## D3 Tutorial 

Follow the tutorial linked below. This tutorial covers some of the core concepts and work flows of D3. 

https://github.com/Tech-at-DU/d3-tutorial

<!-- > -->

## Choosing a Dataset

You'll need your own dataset soon — for [Visualization 1](../Assignments/assignment-2.md) — so start thinking about it now, while you're still working through the D3 tutorial. Having a real dataset in hand makes the tutorial's examples click faster too, since you can try things against your own data as you go.

### What makes a good first dataset?

- **It's tabular** (or close to it) — a list of records where each record has the same fields, like the Titanic passenger list from [lesson-03](./lesson-03.md). Deeply nested or inconsistent data is harder to work with; save that for once you're more comfortable.
- **It has a mix of field types** — at least one categorical field (a category, a country, a gender) and one or two numeric fields (a price, an age, a rating). Categorical fields make good axes, groups, or colors; numeric fields make good lengths, positions, or sizes.
- **It answers a question you actually care about.** You'll be staring at this data for a while — pick something you're curious about, not just the first result you find.
- **It's documented.** Good datasets on Kaggle describe what each column means. If you can't tell what a column represents, you can't visualize it honestly.

### File size — how much can a browser handle?

Your data has to be downloaded and parsed in the browser before you can draw anything with it, so size matters more here than it would on a backend.

Rough guidelines:

- **Under 100KB** — no problem, loads instantly.
- **100KB – 1MB** — still fine for a `fetch()` + parse on page load. This is the sweet spot for a class project.
- **1MB – 5MB** — workable, but you'll notice the load/parse time, especially on a slow connection or an older machine. Better to trim it down first (see below) than ship the whole thing.
- **5MB+** — don't load this directly in the browser. Preprocess it down to what you actually need and load that smaller file instead.

**Aim for 1MB or smaller.** When you filter datasets on Kaggle, use its file-size filter to rule out anything bigger before you even open it.

### File formats

- **CSV** — smaller on disk, flat (one row per record, no nesting), easy to eyeball in a spreadsheet before you write any code. D3 loads it with `d3.csv()`.
- **JSON** — larger on disk but maps directly onto JS objects/arrays and can express nested structure. D3 loads it with `d3.json()`; with `fetch` it's just `.then(r => r.json())` — no separate parsing step.
- **GeoJSON / TopoJSON** — if you're building a map you'll need one of these for the shapes, on top of whatever data file drives the colors/values. See [lesson-13](./lesson-13.md).

See [lesson-03: CSV vs JSON](./lesson-03.md#csv-vs-json) for the full tradeoff between the two.

### Working with a big dataset: pull a smaller slice

Found a dataset you love, but it's 20MB and covers 50 years? Don't load all of it — cut it down to what your visualization actually needs, and load only that:

- **Filter rows** — one year instead of fifty, one country instead of every country, one category instead of all of them.
- **Drop columns you won't use** — if the dataset has 40 columns and you're visualizing 3 of them, don't ship the other 37.
- **Sample** — if you just need "enough data to look real," take every Nth row, or a random sample of a few thousand rows instead of a few million.
- **Aggregate first** — if your chart shows totals or averages *by category*, you don't need every raw row. Group and summarize once, save that smaller result, and load that instead of the raw records.

You don't have to do this trimming in the browser. Write a small script (Node, Python, even a spreadsheet) that reads the big file, filters/aggregates it, and writes out a small JSON or CSV file — that smaller file is what your visualization actually loads.

<!-- > -->

## After this lesson

- Finish the [D3 tutorial](https://github.com/Tech-at-DU/d3-tutorial)
- Move on to [lesson-11](./lesson-11.md) (D3 Scales), and keep narrowing down the dataset you'll use for Visualization 1
