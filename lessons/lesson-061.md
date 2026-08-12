
# ACS 4310 - Canvas Part 2, Circle Math

## Overview

Today we'll learn how to draw circles and calculate coordinates on circles.

### Why?

Circles are used all the time in visualizations (pie chart, scatter plot, dot plot, cluster analysis, etc.) and it's important to know how to draw them in order to properly convey your analysis.

Plus they're cool!

<!-- > -->

## Learning Objectives

- Use Math functions and simple trigonometry
	- `Math.PI`
	- `Math.sin(radians)` -1 to +1
	- `Math.cos(radians)` -1 to +1

<!-- > -->

## Intro

Sometimes you'll want to place things in a circle. Imagine the numbers around a clock. If you had to make this yourself you'd need to place each of the numbers equally spaced around a center point.

To do this, use `Math.sin()` and `Math.cos()`. Each of these takes a value in radians and return a number between -1 and +1. Multiply the return value by the radius.

A full circle is `Math.PI * 2`.

Think about the clock. To get the position of each hour divide the circle by 12.

`const step = Math.PI * 2 / 12`

<!-- v -->

Decide what the radius of your clock face is. Imagine it's 200px.

```JS
const numbers = [1,2,3,4,5,6,7,8,9,10,11,12]
const step = Math.PI * 2 / numbers.length
const radius = 200
numbers.forEach((n, i) => {
	const x = Math.sin(step * i) * radius
	const y = Math.cos(step * i) * radius

	// draw number at x, y
})
```

The center of the clock face would be at 0, 0 with the numbers arranged in a 200 pixels radius circle around that point. Imagine the center of the clock in the upper left corner.

You usually don't want to place everything in the upper left corner. To move the center of the clock face anywhere on the canvas you'll need to offset the x and y values.

<!-- v -->

```JS
const numbers = [1,2,3,4,5,6,7,8,9,10,11,12]
const step = Math.PI * 2 / numbers.length
const radius = 200
const offsetX = 300
const offsetY = 250
numbers.forEach((n, i) => {
	const x = Math.sin(step * i) * radius + offsetX
	const y = Math.cos(step * i) * radius + offsetY

	// draw number at x, y
})
```

Just add the offset to the x and y. In this case the center of the clock face is at 300, 250 on the canvas.

<!-- > -->

## Where this is used

This is the math behind arranging the frequency bars radially in the [Real-Time Audio Visualizer](../Assignments/assignment-3.md) bonus project (see [lesson-07](./lesson-07.md)). It also comes up any time you need to lay elements out in a circle or ring — radial bar charts, pie/donut labels, clock-style dashboards.

## Additional Resources

- [lesson-06](./lesson-06.md) - Canvas basics
- [Sine/Cosine](https://en.wikipedia.org/wiki/Sine)
