# Assignment 3 (Optional Bonus) - Real-Time Audio Visualizer

This assignment is **optional**. It's not required to pass the course, but it's a fun, well-supported project if real-time/generative visuals interest you — and it can stand in as one of your three required visualizations from [Assignment 2](assignment-2.md) if you'd rather build this than a third dataset-driven chart.

## Goal

Build an audio visualizer with JavaScript: draw live audio data onto a `<canvas>` element.

The Web Audio analyzer provides an array of 1024 8-bit integers, one per frequency band, each 0–255 representing how loud the audio is in that band at that instant. Your job is to turn that array into something drawn on canvas.

## Learning Objectives

- Use canvas to display data
- Draw data in real time
- Normalize values from one range into another

## Getting started

Follow the tutorial and notes in [lesson-07](../lessons/lesson-07.md) and [lesson-061](../lessons/lesson-061.md) (canvas + circle math). Sample starter code:

https://github.com/Tech-at-DU/ACS-4310-real-time-visualization

## Challenges

**Challenge 1** — Follow the tutorial and get the base visualizer working.

**Challenge 2** — Design the page: modify the HTML and CSS around the visualizer.

**Challenge 3** — Make the drawing itself your own. Change at least:

- the color of the lines or fills
- the geometry of the lines and fills
- the line width

This part is open-ended — take it in whatever direction interests you and matches your ability level. By the end you should have a visualizer that looks nothing like the tutorial's example.

## Submission

Submit your GitHub repo link to GradeScope.

## Evaluate your progress

| Expectation | Does not meet | Meets | Exceeds |
|:-------------|:------------------|:----------------|:-----------------|
| **Completion** | Visualizer doesn't work, or looks identical to the tutorial | Visualizer works and has a unique appearance | Patterns displayed are fun and interesting enough that people comment when they see it |
| **Code quality** | Sloppy, unorganized, throws errors or warnings | Well organized, works without errors | No linter errors or warnings |

Learning Objectives

| Expectation | Does not meet | Meets | Exceeds |
|:-------------|:------------------|:----------------|:-----------------|
| **Canvas** | Can't explain canvas | Can explain canvas | Can explain canvas and several of its commonly used methods |
| **requestAnimationFrame** | Can't explain `requestAnimationFrame()` | Can explain `requestAnimationFrame()` | Could apply `requestAnimationFrame` to another project where appropriate |
