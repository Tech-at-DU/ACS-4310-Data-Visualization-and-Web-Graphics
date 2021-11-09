
# ACS 4310 - Canvas, math, and Audio

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
- Use the audio object
- draw real-time data

<!-- > -->

## Real-Time Data

Real-time data is data that changes from moment to moment, micro-second to micro-second even! 

This can be stock prices, exchange rates, interstellar noise, tectonic motion, heart rates, and more. For this project you will work with audio data. 

<!-- > -->

## Getting started 

Create a new folder for this project. Add an HTML file with two elements: 

```HTML
<canvas id="canvas" width="300" height="300"></canvas>
<button id="button-play">Play</button>
```

The canvas will display the visualization and the button will be used to start playing the audio.

Canvas is a good choice for real time data since it allows us to draw to the screen faster than than updating the DOM. Drawing to canvas is a single step process. Where updating the DOM requires the browser to traverse the DOM tree and update all child nodes when a change is made. 

## Audio

The Audio Object loads audio data. The Audio object does many things. It can play and modify audio and generate new audio sources and process audio. You can make a whole audion workstation with JS! 

It can also analyze audio and provide information about the audio source. This what you are are going to do with this project. 

### Load Audio 

The code snippet below uses the Audio object to load a sound file and play it.

```JS
function startAudio() {
  // Create an Audio instance 
  const audio = new Audio()
  // Make a new Audio Context
  const audioContext = new (window.AudioContext || window.webkitAudioContext)()
  // Set the src to a sound file
  audio.src = 'bird-whistling-a.wav'
  // Play the audio
  audio.play()
}
```

Call the function above with a button: 

```JS
const playButton = document.getElementById('button-play')

playButton.addEventListener('click', (e) => {
  startAudio()
})
```

**You can't play audio without user interaction** Read this rationale https://developers.google.com/web/updates/2017/09/autoplay-policy-changes

<!-- > -->

### Analysing Audio

The Audio object can do many things with an audio source. Think of the Audio object as processing plant for sound. It allows you to process audio by passing it through nodes. The nodes process the audio from the previous node.

You can do things like: 

- Filter sound (think equalizer)
- Mix sounds
- Split sound into stereo
- Create effects like echo
- Increase or decrease the gain of sounds
- Create an oscillator (sound generator)
- Pan sounds from left to right
- Analyze audio
- and more...

Seriously you can make your own digital audio workstation with JavaScript in the browser. Take a look at BandLab.com it like GarageBand meets GitHub in the browser. 

For your visualization, you need to create an analyzer. An analyzer looks at a snapshot of audio and provides an array of numbers that represent how loud the sound is at that moment in 1024 frequency bands.

Add two variables to hold a reference to the analyzer and 

```JS
let analyser
let frequencyArray

function startAudio() {
  ...
}
```

Add a couple of lines of code to your 

```JS
function startAudio() {
  const audio = new Audio()
  const audioContext = new (window.AudioContext || window.webkitAudioContext)()

  audio.src = 'bird-whistling-a.wav'

  // --------------------------------------------------------
  // Create an audio analyser
  analyser = audioContext.createAnalyser()
  // Create an audio source
  const source = audioContext.createMediaElementSource(audio)
  // Connect the source to the analyser
  source.connect(analyser)
  // Connect the analyser to the audio context
  analyser.connect(audioContext.destination)
  // Get an array of audio data from the analyser
  frequencyArray = new Uint8Array(analyser.frequencyBinCount)
  // --------------------------------------------------------

  audio.play()
}
```

Here you created an analyser and a source. Then you connected the two and then connected the analyser to the audio context created earlier. Last you got an array of frquency data from the analyser. 

Don't worry about fully understanding everything that is happening here. For what you are working on if everything else works the one line that is most important is the last one. This is the line supplies the data you will work with to visualize. 

This last line generates an array of 1024 8 bit values. That is it's an array of 1024 numbers that all range from 0 to 255. The value of each represents how load the audio is in each of the 1024 frquecy bands. 

You'll need to run this last line of code each time you want to update your visualization. At each moment the audio plays the frequency information changes. You'll need to refill the frequency array with new values each time you want to update the vidsualization. 

## Audio Data 

WHat is this audio data? It's array of numbers. There are 1024 values and each is a value from 0 to 255. 

This gives you the follow information to work with: 

- the index of the value in the array an integer from 0 to 1023
- the value a number from 0 to 255

The index of the value is important since it represents the frequency band the value represents. Low frequencies are lower numbers and the highest frequencies are at the end of the array.

So you have two numbers to work with. 

The index value is good for an x or y value. You can divide anything into 1024 slices. For example if you wanted to create a row of vertical lines, you would have 1024 lines. If your canvas was 600px wide each line would be positioned 600 / 1024 pixels apart. 

You can use the same idea in another way. By normalizing values to a range of 0.0 to 1.0 you can scale them to any range. For example we're starting with valeus from 0 to 255. Taking one of these values and dividing by the maximum you get a normalized value. From here you can multiply by any other value to get a range of that value. 

Let's take that last idea into a practical example. Imagine you have frquency data in the range of 0 to 255 and your canvas is 300 pixels tall. 

```JS
const f1 = 128
const f2 = 0 
const f3 = 255

f1 / 255 * 300 // 150
f2 / 255 * 300 // 0
f3 / 255 * 300 // 300
```

What happened above? f1 is 128, divided by 255 is 0.5, multipplied by 300 is 150. The forumla tranlates the frquency range of 0 to 255 into a range of 0 to 300. Imagine that your canvas is 300 pixels tall, here you would translating the frequency to a range in pixels. 

### Rendering Audio

To draw the visualization in real time you need to update the screen periodically. For this you'll use: `requestAnimationFrame()`. This method will call a callback once just before the browser is ready to draw the screen. 

On a new animation frame you'll get the audio frequency data, loop over the data and use it to draw something on a canvas. Then setup a new requestAnimationFrame callback that will start the process again in a fraction of a second. 

The process of rendering audio will follow these steps: 

- Clear the canvas 
- Get an array of frequency values from the analyzer
- For each frequency in the array
  - Use each value to draw something on canvas

All of the steps above will be repeated each time the browser redraws. 

Add some references to the canvas and some variables we can use for drawing. 

```JS
const canvas = document.getElementById('canvas')
const ctx = canvas.getContext('2d')

const centerX = canvas.width / 2
const centerY = canvas.height / 2
const radius = canvas.width / 5
```

Add a new function: 

```JS
function render() {
  // ...
  requestAnimationFrame(render)
}
```

You need to call this `render()` function from `startAudio()` to begin rendering the visualization. 

```JS
function startAudio() {
  ...

  render()
}
```

Back in the `render()` function add a few lines to clear the canvas and draw a circle in the center.

```JS
function render() {
  // -----------------------------------------------
  ctx.clearRect(0, 0, 300, 300)
  ctx.beginPath()
  ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI)
  ctx.strokeStyle = 'red'
  ctx.stroke()
  // ----------------------------------------------

  requestAnimationFrame(render)
}
```

Define a couple of variables that will be used to draw the bars. 

Get an array of frequencies from the analyzer. 

```JS
function render() {
  ctx.clearRect(0, 0, 300, 300)
  ctx.beginPath()
  ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI)
  ctx.strokeStyle = 'red'
  ctx.stroke()

  // -------------------------------------------------
  const bars = 200
  const step = Math.PI * 2 / bars

  analyser.getByteFrequencyData(frequencyArray)
  // --------------------------------------------



  requestAnimationFrame(render)
}
```

For each frequency, you'll draw a line. To do this we need to the starting point: x1 and y1, and the ending point x2, y2. Each line is drawn as a path the last step is to stroke the paths. 

```JS
function render() {
  ctx.clearRect(0, 0, 300, 300)
  ctx.beginPath()
  ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI)
  ctx.strokeStyle = 'red'
  ctx.stroke()

  const bars = 200
  const step = Math.PI * 2 / bars

  analyser.getByteFrequencyData(frequencyArray)

  // --------------------------------------------
  frequencyArray.forEach((f, i) => {
    const barLength = frequencyArray[i] * 0.5
    const x1 = (Math.cos(step * i) * radius) + centerX
    const y1 = (Math.sin(step * i) * radius) + centerY
    const x2 = (Math.cos(step * i) * (radius + barLength)) + centerX
    const y2 = (Math.sin(step * i) * (radius + barLength)) + centerY

    ctx.moveTo(x1, y1)
    ctx.lineTo(x2, y2)
  })

  ctx.stroke()
  // -------------------------------------------------

  requestAnimationFrame(render)
}
```

### Challenges 

1. Follow the tutorial steps above and get this working.
2. Customize the drawing code from the last step.
 - Change the color.
 - Change the color of each line. To do this you'll need to: 
 - set the `ctx.strokeStyle` inside the loop and call `ctx.stroke()` inside the loop.
 - Change the lines drawn. Currently they are mapped around the circle. Change the x1, y1, and x2, y2 values to something else.
 - Draw rectangles or circles. Draw one circle for each frequency. You could set the width, height, or radius based on the frequency value. 

### Sample code 

Take a look at the sample code here: 

https://github.com/Tech-at-DU/ACS-4310-real-time-visualization

<!-- .slide: data-background="#087CB8" -->
## [**10m**] BREAK

Take a 10 minute break

## After Class

- [Audio Visualization](assignments/assignment-3.md)
- Due Feb. 17 
- Submit your GitHub Project via GradeScope

<!-- > -->

## Additional Resources

- https://github.com/Tech-at-DU/ACS-4310-real-time-visualization
- https://www.kkhaydarov.com/audio-visualizer/
- https://medium.com/@duraraxbaccano/computer-art-visualize-your-music-in-javascript-with-your-browser-part-2-fa1a3b73fdc6



















<!-- Put a link to the slides so that students can find them -->
<!-- 
➡️ [**Slides**](https://make-school-courses.github.io/FEW-2.5-Data-Visualization-and-Web-Graphics/Slides/Lesson-6.html ':ignore') -->

<!-- > -->

## Overview

This class will be a workshop to work on and finish up the audio visualizer project and study the Math of Circles. 

### Why?

Circles are used all the time in visualizations (pie chart, scatter plot, dot plot, cluster analysis, etc.) and it's important to know how to draw them in order to properly convey your analysis.

Plus they're cool!

<!-- > -->

## Learning Objectives

- Use Math functions and trigonometry
- Draw images with circles and code

<!-- > -->

## Intro

Sometimes you'll want to place things in a circle. Imagine the numbers around a clock. If you had to make this yourself you'd need to place each of the numbers equally spaced around a center point.

Imagine you know where the center of the circle is and imagine that it is x 0 and y 0. To place the 12 it would be 0 x and y - the radius of the circle. For the 3, 6, and 9 you could follow a similar pattern. 

When it's time to place the 1, 2, 4, and other numbers it's hard to caluclate the their x and y. 

There are a few Math functions that can help with this.

You are probably used to looking at a circle as 360 degrees. In trigonmetry we look at a circle radians. There are  Pi radians in a circle. Or you could think of 2 Pi as 360 in degrees.

`Math.sin()` and `Math.cos()` can be used to map an x and y value from radians. Each of these functions takes a value in radians and return a number between -1 and +1. Multiply the return value by the radius to get the x and y around the center.

Think about the clock. To get the position of each hour divide the circle by 12.

`const step = Math.PI * 2 / 12`

<!-- v -->

Decide what the radius of your clock face is. Imagine it's 200px.

```JS
const numbers = [3,4,5,6,7,8,9,10,11,12,1,2]
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



<!-- ## Playing with Circles

Check out the [Example code](../lesson-06.html) linked here and see how you can manipulate the circles!  -->

<!-- > -->

<!-- .slide: data-background="#087CB8" -->
## [**10m**] BREAK

Take 10 minute break

<!-- > -->

## Lab

Continue working on the audio visualizer project. 

Use the lab to time complete the challenges and stretch challenges. 

<!-- > -->

## After class

- Continue working on - [Audio Visualization](../Assignments/assignment-3.md) submit your completed work to GradeScope. 

<!-- > -->

## Additional Resources

- [Sine/Cosine](https://en.wikipedia.org/wiki/Sine)

<!-- > -->

## Minute-by-Minute

<!-- 
| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:30      | In Class Activity I       |
| 0:50        | 0:10      | BREAK                     |
| 1:00        | 0:45      | In Class Activity II      |
| 1:45        | 0:05      | Wrap up review objectives |
| TOTAL       | 1:50      | -                         | 
-->
