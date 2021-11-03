
# ACS 4310 - Canvas

<!-- Put a link to the slides so that students can find them -->

<!-- ➡️ [**Slides**](https://make-school-courses.github.io/FEW-2.5-Data-Visualization-and-Web-Graphics/Slides/Lesson-7.html ':ignore') -->

<!-- > -->

## Overview

Sometimes data changes moment by moment. The goal of this nest assignment is to display data in real time. 

<!-- > -->

## Why you should know this?

Experimenting with real-time data is expands your skills into new areas. Tracking frame updates and working with canvas and large datasets. 

<!-- > -->

## Learning Objectives

- Use canvas to draw data
- draw real-time data

## canvas

Canvas is a an HTML elment that allows you to draw with pixels. Think of it like an image but the image is generated with code. 

Canvas has the advantage that drawing pixels is a faster process than drawing objects. Objects have a lot of meta data and rules that come with them and need to be further processed before they can be turned into pixel data. 

Canvas bypasses all of this process and provides you with tools for drawing pixel data directly to the page. 

### Why use canvas?

Canvas isn't good for everyday processes where you have specialized elements. For example, you wouldn't want to use canvas to draw text or headings. Though canvas can draw text, it doesn't not allows us to select and copy the text or style it with CSS. Instead we have the `<p>`, `<h1>`, and other tags that supply this functionality. 

So why use canvas? Canvas is great when you need to draw raw pixels to the screen directly. This is good for things like games where performance is important. It's also good for real time process like drawing audio wave forms or other things that update quickly and need to be drawn fast. 

Canvas is also good when you need to make custimized drawings. HTML elements are limited in what you can draw with them. With canvas you can draw just about anything! 

## Using canvas 

To use canvas follow these steps:

- Create a canvas element, be sure to set it's width and height
- Get a reference to the canvas element
- Get the canvas context, this object cantains all of the drawing methods
- Use the canvas methods and properties to draw on the canvas

Here is how it would look in code. 

Create a canvas element in your HTML document. 

```HTML
<canvas width="600" height="400"></canvas>
```

In your JS get a reference to the canvas and use that to get the context. 

```JS
const canvas = document.querySelector('canvas')
const ctx = canvas.getContext('2d')
```

The canvas context `ctx` above, has many properties and methods that can draw things in many ways. You'll follow roughly these steps: 

```JS
// Draw a box
ctx.beginPath()
ctx.fillStyle = 'tomato'
ctx.rect(20, 120, 200, 150)
ctx.fill()
ctx.closePath()
```

Here we follow these steps. 

- Begin a new path. Think of a path as a line that you can later stroke and or fill with colors. 
- Set the fill style. This can be any color written as a CSS color. 
- Draw a rectangle path. Here we draw a rectangular path the four values are the x and y position of the upper left corner followed by the width and height. 
- Fill the path. Here we fill the path with a color set by the fill style. 
- Last close the path. This step allows you to start a new path and fill or stroke the new path with different colors. 

Here are some examples: 

```JS
// Draw a circle witha fill and a stroke
		ctx.beginPath()
		ctx.fillStyle = 'cornflowerblue'
		ctx.strokeStyle = 'brown'
		ctx.lineWidth = 7
		ctx.arc(300, 200, 75, 0, Math.PI * 2)
		ctx.fill()
		ctx.stroke()
		ctx.closePath()

		// Draw a line 
		ctx.beginPath()
		ctx.strokeStyle = 'lime'
		ctx.lineWidth = 20
		ctx.lineCap = 'round'
		ctx.moveTo(30, 200)
		ctx.lineTo(570, 30)
		ctx.stroke()
		ctx.closePath()
```

In the second example we draw a stright line. Notice here we used `ctx.moveTo()` to move the drawing context to a starting pposition for the line. This doesn't draw anything! Then we use to `ctx.lineTo()` to draw a line from that starting position. Both `moveTo(x, y)` and `lineTo(x, y)` take the x and y coordinates. 

### Drawing a collection of data

Often you'll have an array of values that you'll want to display. If you have an array of numbers you can work with both the value in the array and the index of that value! 

In the example below I generated an array of 300 random numbers and draw a line connecting each. 

```JS
// make an array of 300 random values
const noise = []
// Generate 300 random values
for (let i = 0; i < 300; i += 1) {
  noise.push(Math.random() * 400)
}

// Move the drawing context to the position of the first value
ctx.moveTo(0, noise[0])
ctx.beginPath()
ctx.strokeStyle = 'black'
ctx.lineWidth = 1
// Loop over the values and draw lines
noise.forEach((y, i) => {
  // calculate x with i
  const x = i * 2
  ctx.lineTo(x, y)
})
ctx.stroke()
ctx.closePath()
```

### Normalizing data

Most often the dat you get will not fit the range that is needed to draw it. In the example above the random numbers were in the range of 0 to 400.This fit perfectly to our canvas height of 400. 

What if the range of values was in the range of 0 to 255 can your canvas was 400 pixels tall? In this case you need to scale the numbers to fit. 

This is the process of normalizing. Divide all of the values by the largest value in the range: 255 in this case. That should convert each value into a range of 0.0 - 1.0. Then multiply by your target range 400 in this case. 

Here is an example: 

```JS
// make an array of 300 random values
  const noise2 = []
  for (let i = 0; i < 300; i += 1) {
    // vall values should be 0 to 255
    noise2.push(Math.random() * 255)
  }

  // Move the drawing context to the position of the first value
  
  ctx.beginPath()
  ctx.moveTo(0, noise2[0])
  ctx.strokeStyle = 'red'
  ctx.lineWidth = 3
  // Loop over the values and draw lines
  noise2.forEach((val, i) => {
    const x = i * 2
    // Since the source values range from 0 - 255
    // and the canvas is 400 pixels tall we need to 
    // normalize and offset the values.
    const y = val / 255 * 400
    ctx.lineTo(x, y)
  })
  ctx.stroke()
  ctx.closePath()
```

### Offset values

Some times you'll need to offset a value. Imagine the values you get are in the range of -1 to +1. If you normalize these some of the values will be negative. The x and y positions visible on the canvas are all in the positive numbers. 

To offset just add value to bring you number into the positive region. The example below draws a sine wave. The source values are in the range of -1.0 to +1.0. I want to scale them to -100.0 to +100.0. 

In this case half of the value would be off the top of the screen. To move the sine wave to the center of the screen I'll add half the height or 200. Now the range becomes +100.0 to +300.0.

```JS
const sine = []
for (let i = 0; i < 300; i += 1) {
  // vall values should be -1.0 to +1.0
  sine.push(Math.sin(i * 0.05))
}

// Move the drawing context to the position of the first value

ctx.beginPath()
ctx.moveTo(0, sine[0])
ctx.strokeStyle = 'gray'
ctx.lineWidth = 15
// Loop over the values and draw lines
sine.forEach((val, i) => {
  const x = i * 2
  // Since the source values range from 0 - 255
  // and the canvas is 400 pixels tall we need to 
  // normalize and offset the values.
  const y = (val * 100) + 200
  ctx.lineTo(x, y)
})
ctx.stroke()
ctx.closePath()
```

<!-- > -->

## Additional Resources

- https://github.com/Tech-at-DU/ACS-4310-real-time-visualization
- https://www.kkhaydarov.com/audio-visualizer/
- https://medium.com/@duraraxbaccano/computer-art-visualize-your-music-in-javascript-with-your-browser-part-2-fa1a3b73fdc6

<!-- > -->

<!-- ## Minute-by-Minute

| **Elapsed** | **Time** | **Activity** |
| ----------- | --------- | ------------------------- |
| 0:00 | 0:05 | Overview and Learning Outcomes |
| 0:05 | 0:10 | CDNs |
| 0:15 | 1:00 | ChartJS |
| 1:15 | 0:10 | BREAK |
| 1:25 | 1:15 | Lab |
| 2:40 | 0:05 | Wrap up and review homework |
| TOTAL | 2:45 | - |
 -->
