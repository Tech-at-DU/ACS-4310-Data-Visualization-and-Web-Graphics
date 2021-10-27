# ACS 4310 - Making data visible

Making data visible with HTML, CSS, JavaScript. 

<!-- Put a link to the slides so that students can find them -->

<!-- ➡️ [**Slides**](https://make-school-courses.github.io/FEW-2.5-Data-Visualization-and-Web-Graphics/Slides/Lesson-4.html ':ignore') -->

<!-- > -->

## Overview

In the last lesson you organized and extracted values from a dataset. The next step is to make this data visible. The goal now is take all of the values and turn them into something that can be displayed. 

<!-- > -->

## Why is this important?

Turning data into something that people can easily understand is why we make websites! 

<!-- > -->

## Learning Objectives

- Create HTML elements with JavaScript 
- Use JavaScript to style elements
- Use Map to transform data into HTML elements

## Infographic vs Data Visualization

Your goal is to make a **data visualization**. This is an or visual representation of data. It's not an info graphic or generative art though all three are related. Take a look at the two articles below for examples of info graphics and data visualizations. 

Take a look at these examples:

- [Info Graphic](https://venngage.com/blog/what-is-an-infographic/)
- [Tableau Best Data viz examples](https://www.tableau.com/learn/articles/best-beautiful-data-visualization-examples)

More Examples: 

- Data visualizations Examples
	- [the psychology behind data visualization](https://treehousetechgroup.com/the-psychology-behind-data-visualization/)
  - [Best Data Visualizations 2018](https://visme.co/blog/best-data-visualizations/)
  - [James Round](https://www.jamesrounddesign.com)
  - [Data visualization](https://datavizcatalogue.com)
  - [Examples](https://www.maptive.com/17-impressive-data-visualization-examples-need-see/)
- Generative art and Data: 
	- https://www.ted.com/playlists/201/art_from_data
	- https://joshuadavis.com
	- https://www.theatlantic.com/entertainment/archive/2015/05/the-rise-of-the-data-artist/392399/
	- https://techcrunch.com/2016/05/08/the-digital-age-of-data-art/

## Revealing a story with data

Your goal is to reveal a story from the data. Look at the provided data and think about how you can express it. For example you can show numbers and text. You can also show visual object on the screen. 

I'd like you to use a combination of generative art and data to make a visualization that reveals some interesting details about the Titanic sotry. 

## Making Data Visible

The goal of this section it display the Titanic data with HTML, CSS and JS. You'll do everything with the code you write. Later we will use code libraries to to more. Writing the code yourself is important to understand programming, problem solving, and a step along the way to writing you writing your own libraries.

These examples can be applied and tested in this Repl.it:  

https://repl.it/join/gnjigkyl-mitchellhudson

## Creating HTML elements

You can generate HTML elements with code! 

```JS
// Creates a new <div>
const el = document.createElement('div')
```

An element is not displayed unless it is added to the DOM

```JS 
// Add the element to the body
document.body.appendChild(el)
```

To visualize the Titanic data you might make an element for each passenger. 

```JS
const passengers = data.map(p => {
  const el = document.createElement('div')
  titanic.appendChild(el)
  return el
})
```

The pasengers array now contains a collection of `<div>` elements. In order to make these element visible they need to be added to the DOM. Line 2 does this. 

Sotring the elements in an array allows you to loop over the array and set properties on each of the elements. In this way you can modify the elements to control their appearance. 

## Styling HTML Elements 

All CSS styles can be applied in via code. All CSS style properties are available through JavaScript. 

Set any property on an elements style property. All CSS property names convert to camel for their JS name. 

Since CSS values usually include a unit you'll always use a string when setting the value in JS. 

```JS
// set the width and height
el.style.width = '100px'
el.style.height = '200px'
// Set the background-color
el.style.backgroundColor = '#f0f'
// Make an element display as a grid
el.style.display = 'grid'
el.style.gridTemplateColumns = 'repeat(6, 100px)'
el.style.gridGap = '2px'
```

You can style all of the passenger elements using `passengers.forEach()`. 

```JS
passengers.forEach((p, i) => {
  p.style.width = '10px'
  p.style.height = '10px'
  p.style.backgroundColor = '#000'
})
```

Here each of the pessengers was styled with a width and height of 10px, and a background color of black. 

The index of each passenger matches the index of an object in the data array. You can use this to make styles that are influenced by the data. 

Imagine you want to set the opacity of each element based on whether that passenger survived or not. 

```JS
passengers.forEach((p, i) => {
  const { survived } = data[i].fields // Get the relevant property
  p.style.width = '10px'
  p.style.height = '10px'
	// Set a value based on the property
  p.style.opacity = survived === 'Yes' ? '100%' : '50%' 
  p.style.backgroundColor = '#000'
})
```

### What types of styles?

So what types of styles can you use? You can use all of them! There is a limit to what we can draw with HTML and CSS alone. An element generally displays as a box. Here are some suggestions for properties you might set: 

- `backgroundColor` 
- `opacity`
- size: `width` and `height`
- `border`, width, color, style, radius

What can you draw with these properties? It seems limited but there are lots of possiblities. You can use different properties to represent different aspects of the data.

The possibilities open up when you combine elements. Imagine that each of the divs in the passengers array also had another div inside. 

## After Class

- https://github.com/Tech-at-DU/Visualize-Titanic

## Video lessons

- https://youtu.be/BgCRqcwZ4TA
- https://youtu.be/iwYmA0HISSQ
- https://youtu.be/SxNpz23yaKs
- https://youtu.be/lNPbtl0K860

<!--

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Overview and Learning Outcomes                |
| 0:05        | 0:15      | Distributions                  |
| 0:20        | 0:10      | Sorting       |
| 0:30        | 0:10      | Filtering                     |
| 0:40        | 0:15      | Holding Elements      |
| 0:55        | 0:15      | Animations      |
| 1:10        | 0:15      | CSS Transforms      |
| 1:25        | 0:10      | Closures      |
| 1:35        | 0:10      | BREAK      |

-->