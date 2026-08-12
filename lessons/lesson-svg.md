
# ACS 4310 - SVG

## Overview

Scalable Vector Graphics (SVGs) are written in a language like HTML and produce images on the screen. They also support many other features, can be styled with CSS, and manipulated with JavaScript.

<!-- > -->

## Why you should know this

You should learn them because they an important tool that will give you more capabilities and more answers to development problems you will encounter in the future.

<!-- > -->

## Learning Outcomes

- Understand the benefits and drawbacks to using SVGs
- Practice working with SVGs to make data visualizations

<!-- > -->

## SVG

SVG is a file format and a language. You can create SVG files in popular apps like Sketch.

Think of SVG as a language that describes a drawing. The computer reads an SVG file calculates the shapes and paths in the description, then fills the shapes and strokes the paths with pixels.

<!-- v -->

**Pros:**

- Smaller file size
- Separate elements
- Elements are accessible from code
- Crisp and scalable/responsive images

**Cons:**

- More processor overhead
- Images can't create some detail available to raster images

<!-- > -->

## Working with SVG

You can save the files and import them like images.

`<img src="my-image.svg">`

When using SVG in this way images are rendered but you don't have access to underlying SVG code.

<!-- v -->

You can also use SVG code directly in your work. just copy and paste some SVG code into an HTML document or write the code from scratch!

```SVG
<svg width="454px" height="432px" viewBox="0 0 454 432" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
        <polygon id="Star" stroke="#FFCC00"
        stroke-width="43" fill="#FF9500"
        points="227 334 115.320802 392.713229
        136.649631 268.356614 46.2992619
        180.286771 171.160401 162.143386 227 49
        282.839599 162.143386 407.700738
        180.286771 317.350369 268.356614
        338.679198 392.713229"></polygon>
    </g>
</svg>
```

The code above draws a star.

<!-- v -->

Generally speaking you usually don't want to write SVG code from scratch. Instead, use an application such as Sketch.

Here's some guidelines to consider when working with SVGs:

- If you need to make a drawing of something like a logo or icon use Sketch.
- If you need to generate shapes dynamically, use a library.

<!-- > -->

## After this lesson

SVG is one more tool in the kit for your [three visualizations](../Assignments/assignment-2.md) — D3 builds most of its output as SVG under the hood, so this is worth understanding even if you never hand-write SVG directly.

## Additional Resources

- [MDN: SVG](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [lesson-09](./lesson-09.md) - D3, which generates SVG for you
