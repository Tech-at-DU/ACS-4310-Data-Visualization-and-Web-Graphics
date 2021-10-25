
# ACS 4310 - Historgrams

Telling stories with data. 

<!-- > -->

## Historgrams 

A histogram represents the distribution of data. A histogram divises values into bins or buckets. The idea is to count how many values are in each bin. 

This can tell you how many, how much, or how frequently values appear. 

For example. If we were curious about how money people were willing to spend on lunch a histogram might be a good way to look at the problem. This might be useful for our new lunch delivery app. 

Imagine a list of numbers that represent the amount our subject group spends on lunch. 

```JS
[14.54, 8.54, 10.00, 12.30, 9,76, 5.65, 7.85, 5.50, 23.50]
```

We could divide this group into buckets of $5. 

- 0.00 - 4.99 - 0
- 5.00 - 9.99 - 5
- 10.00 - 14.99 - 3
- 15.00 - 19.99 - 0
- 20.00 - 24.99 - 1

With a histogram we can clearly see most people are spending $5 to $15. If we target below $5 or above $15 we aren't going to have many customers! 

Here is a good explanation of historgrams: https://chartio.com/learn/charts/histogram-complete-guide/

## Making a histogram in code

This is a pretty open ended question. There are many ways to solve this. 

An easy starting point for creating a historgram is an array. Imagine the example above.

```JS
const prices = [14.54, 8.54, 10.00, 12.30, 9.76, 5.65, 7.85, 5.50, 23.50]

/* Imagine we need the output should look like this: 
- 0.00 - 4.99 - 0
- 5.00 - 9.99 - 5
- 10.00 - 14.99 - 3
- 15.00 - 19.99 - 0
- 20.00 - 24.99 - 1
*/

const pricesByBucket = makeHisto(prices, 5)

// [0, 5, 3, 0, 1]
```

To do this the `makeHisto()` needs to look at each value and place it at the correct position in the array. 

```JS
const prices = [14.54, 8.54, 10.00, 12.30, 9.76, 5.65, 7.85, 5.50, 23.50]
// First attempt
const histogram = []
// Loop over the values
for (let i = 0; i < prices.length; i += 1) {
  // get a price
  const price = prices[i] 
  // divide by the step and round down. The tells which bucket
  const index = Math.floor(price / 5) 
	// add one to the bucket
	histogram[index] = histogram[index] !== undefined ? histogram[index] + 1 : 1
}
// Check the results
console.log(histogram) // [ <1 empty item>, 5, 3, <1 empty item>, 1 ]
```

The empty slots represent array indexes that were never assigned a value. If we set a value at index 1

The above example works on the idea that taking a value and dividing it by our step will provide the index which tells which bucket to place it in the array! For example: 

$14.54 / 5 = 2.908 round that down to 2 and we count 1 for bucket 2. The array would look like this: 

```JS
const buckets = []
buckets[2] = 1
console.log(buckets) // [ <2 empty items>, 1 ] 
// The array might look like this: [,,1]
```

After creatng the histogram you'll probably need to fill in the empty slots with 0. JavaScript has some interesting behavior around these empty slots. 

```JS
const buckets = []
buckets[2] = 1
console.log(buckets) // [ <2 empty items>, 1 ] 
// The array might look like this: [,,1]
for (let i = 0; i < buckets.length; i +=1 ) {
	console.log(buckets[i])
}
// Prints:
// undefined
// undeifined
// 1
```

That makes sense. What about `forEach()`?

```JS
buckets.forEach(item => console.log(item))
// Prints:
// 1
```

What happened to the empty slots? `forEach` seems to skip over empty slots in an Array. The same is true for `map`, `filter`, and `reduce`!

They mention it in the docs here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#no_operation_for_uninitialized_values_sparse_arrays

How to fill these empty slots? You can use a for loop like I did above checking each value for `undefined`. Another option is: `Array.from()`. `Array.from()` is a method that creates an array from an array-like object. You can use it to copy an array and fill in empty slots along the way. 

```JS
const filledBuckets = Array.from(buckets, a => a || 0)
// [ 0, 5, 3, 0, 1 ]
```

The second parameter is a callback that allows you to map all values. For each value in the source array the callback is run and the value is passed as an argument. The returned value is added to the output array. Just like map! In this case all of the values are iterated even the empty slots! 

Let's go over that again. A histogram divides a list of values into ranges and counts how many values fall into each range. We can think of range as a bucket. 

One way to make a histogram is to divide values by a step and round down this will give you the index where that value should be counted. 

It is possible that we might end up with empty buckets, or empty slots in our array. In this case we need to fill these with 0 since there were zero values for that bucket. 

## CSV vs JSON

JSON more human readable and works seemlessly with JavaScript because of built in support. 

CSV is notably smaller in file size. It takes fewer characters to express data in CSV format. The JSON sample above is 314 characters, the same data in CSV is only 183 characters. 

JSON has the ability to express structured data. For example a JSON file can express objects and arrays nested within other objects and arrays. CSV has a flat structure and only represents a single level, imagine an array of values (numbers and strings.)

Why use JSON? Use JSON when you need structure beyond a simple array or object. Use JSON when you need seemlessly exchange data with JavaScript programs. 

Why use CSV? Use CSV when you have lots of data and that data is organized in a flat file structure. 

<!-- > -->

## The Titanic Dataset

Take a look at the [Titanic Dataset](https://www.kaggle.com/c/titanic/data). This link points to the Titanic dataset on Kaggle. Kaggle is a web site that shares dtaasets for data science and other studies. 

The Titanic dataset is the starting point for studying dtaascience. It's sort of the Hello World of datsets. It's large enough to provide meaningful information, but also small enough to be managable. 

The Titanic data on Kaggle is in CSV format which makes it harder to work with. You can download the Titanic dataset in JSON here: https://public.opendatasoft.com/explore/dataset/titanic-passengers/export/

Take a look at the data, ask yourself what you see?

- There is a record for each passenger
- Each passenger has fields for a range of data points
 - age, fare, pclass, sex, etc.

What types of values can you find here? 

What could this data tell you? 

Pair and discuss. Come up with a list of things you find interesting. **Write the list on the board.**

<!-- v -->

## Exercise: Finding meaning in Data

The Titanic dataset is an array of objects each of which describes a single passenger. 

What can the array tell you about the Titanic and it's passengers? 

```JS
[{
  "datasetid": "titanic-passengers", 
  "recordid": "398286223e6c4c16377d2b81d5335ac6dcc2cafb", 
  "record_timestamp": "2016-09-20T15:34:51-07:00",
  "fields": {
    "fare": 7.3125, 
    "name": "Olsen, Mr. Ole Martin", 
    "age": 40.0,
    "embarked": "S", 
    "parch": 0, 
    "pclass": 3, 
    "sex": "male", 
    "survived": "No", 
    "ticket": "Fa 265302", 
    "passengerid": 155, 
    "sibsp": 0,
    "cabin": "F4"
  }
},
  {
    ...
  }
]
```

Above is a single passenger what does this tell us about this passenger? 

Name three things you can say about this passenger? 

- ? 
- ? 
- ? 

If we had an array of paessenger what questions could you ask the data? Pair up and make a list of at least 3 questions: 

- ? 
- ? 
- ?

Using the Titanic dataset, you will be practicing the following techniques using JS:

- Counting values - this asks: how many?
- Find the min, max, and median values - this asks: what is the range? 
- Filtering - Looks at subsets of the data
- Aggregate values - Asks how much? and what is the average? 

<!-- > -->

## After Class

Complete the Challenges from lab: [Challenges](https://github.com/MakeSchool-Tutorials/FEW-2-5-Data-Visualization-Working-with-Data/)

- Complete the challenges above and submit your solutions to gradescope.

Video Lessons: 
- https://youtu.be/hRhXWI2IpI0
- https://youtu.be/F3c5tnvODyI
- https://youtu.be/vDIPl9sPeDY
- https://youtu.be/r43ugP5EmtI
- https://youtu.be/xsvLslDQCls
- https://youtu.be/2R_pVXGwApg
- https://youtu.be/cBbcVQm2PK8
- https://youtu.be/RcS51jl-LBg


JavaScript, data visualization, titanic, titanic data, array, map, filter, reduce, callbacks, arrow functions


<!-- > -->

## Additional Resources

- Arrow functions - https://javascript.info/arrow-functions-basics
- Arrays - https://javascript.info/array-methods
- forEach - https://javascript.info/array-methods#iterate-foreach
- Math.max() - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max
- Math.min() - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min

<!--
## Minute-by-Minute

| **Elapsed** | **Time** | **Activity** |
| ----------- | --------- | ------------------------- |
| 0:00 | 0:05 | [Welcome to Data Visualization!](#welcome-to-data-visualization) |
| 0:05 | 0:10 | [Why you should know this or industry application](#why-you-should-know-this-or-industry-application) |
| 0:10 | 0:15 | [Learning Objectives](#learning-objectives) |
| 0:15 | 0:20 | [Overview](#overview) |
| 0:00 | 0:00 | [Arrow Functions](#arrow-functions) |
| 0:00 | 0:00 | [Callbacks](#callbacks) |
| 0:00 | 0:00 | [Arrow function challenges](#arrow-function-challenges) |
| 0:50 | 1:00 | Break |
| 0:20 | 0:25 | [JSON](#json) |
| 0:25 | 0:30 | [CSV](#csv) | 
| 0:30 | 0:40 | [CSV vs JSON](#csv-vs-json) |  
| 0:40 | 0:50 | [The Titanic Dataset](#the-titanic-dataset) | 
| 1:00 | 1:10 | [Exercise: Finding meaning in Data](#exercise-finding-meaning-in-data) |
| 1:10 | 2:00 | [Lab Activity](#lab-activity) |
| 2:00 | 2:10 | [After Class](#after-class) |
| TOTAL | 2:45 | - | 
-->
