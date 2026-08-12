# Assignment 2 - Three Data Visualizations

## Goal

Create **three** data visualizations, each from a dataset of your choice. This is the core project of the course — take each one as far as you can.

## Why this project?

This is your opportunity to practice JavaScript, D3, Canvas, and SVG skills on real data you find interesting. Being able to turn a messy dataset into a clear, honest visual story is a skill that shows up in almost every kind of software job, and it's a strong portfolio piece.

## Choosing datasets

Choose three datasets that are interesting to you. Keep in mind that you'll be loading data into the browser — take note of file size and format before committing to a dataset.

Search [Kaggle.com](https://www.kaggle.com) and filter on format (JSON or CSV) and file size (aim for datasets smaller than 1MB, or plan how you'll trim a larger one down). See [course-requirements.md](../course-requirements.md) for a list of suggested datasets, and [lesson-kaggle](../lessons/lesson-kaggle.md) for tips on evaluating a dataset before committing to it.

## Getting started

Your data will likely need some cleanup before it's ready to display. Some chart types need a plain list, others need a hierarchy or other structure. To reveal a story you may need to sort, filter, or aggregate first — do that work before you start drawing.

You'll also need to decide how each value maps to something visual: an axis, a length, a color, a position. Think this through before you start coding.

## Requirements

For **each** of your three visualizations:

- Ask three questions of the dataset with the goal of telling a story or revealing meaning. For example, using the Titanic dataset you might ask:
	- How many passengers lived and how many died, by gender?
	- How many passengers lived and died, by passenger class?
	- Did having a sibling aboard affect your chance of survival?
- Answer each question with a visualization built from that question. You don't need three separate charts per dataset — one chart can answer more than one question if it's designed well.
- Display, compare, and contrast at least three data points from the dataset (for the Titanic example: age, fare, and embarkation, say).

You can build each visualization using any method covered in the [lessons](../lessons): hand-rolled HTML/CSS/JS, Canvas, SVG, or D3. You don't need to use the same method for all three — pick whatever fits the chart type and dataset best. See [lesson-12](../lessons/lesson-12.md) for help matching a chart type to your data.

## Looking for ideas

Not all charts work for all data. Study these before you commit to a chart type:

- https://www.data-to-viz.com
- https://datavizproject.com

## Example D3 code

- https://github.com/soggybag/d3-examples — line, area, pack, bubble, hierarchy, treemap, pie/arc, axis, scales
- https://github.com/soggybag/FEW-2-5-Data-Visualization-D3 — maps

## Submission

Submit each visualization as its own GitHub repo (or a clearly separated folder in one repo). Post the link(s) to GradeScope.

## Evaluating your work

Apply this rubric to each of the three visualizations:

| Expectation | Does not meet | Meets | Exceeds |
|:-------------|:------------------|:----------------|:-----------------|
| **Dataset** | You don't have a dataset, or it's a poor fit for a chart | Your dataset matches your chosen chart type | You've studied data-to-viz.com to confirm the fit, and understand the dataset's size/format tradeoffs |
| **Details** | You don't know much about the data | Your data is a reasonable size and you understand the values it contains | You've researched the data's history and background |
| **Story** | The chart doesn't reveal anything new about the data | The chart reveals a new idea about the data | The chart tells a story that suggests ideas not apparent in the numbers alone |
| **Technique** | You can't explain or recreate what you built | You can recreate and explain what you built | You could rebuild it with another dataset or chart type |
| **Code quality** | Sloppy, unorganized, throws errors | Well organized, works without errors | No linter errors or warnings |
