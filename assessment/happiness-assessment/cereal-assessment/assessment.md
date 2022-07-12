# Final Assessment

You've just landed a job at a new startup: Brkfst.com. They plan to revolutionize the mornings of everyone around the world by making breakfast fast easy and nutritious!

Currently they have identified cereal as the most popular breakfast food. Their goal is to make the better cereal. 

To do this they need to study the competition. Your job is to create a data visualization that shows the features of the most popular cereal. 

The dataset you have been provided is: cereal.csv. Take a look at it in this directory. You can read more about this dataset here: https://www.kaggle.com/datasets/crawford/80-cereals

It contains the top 80 cereal products with the following data fields: 

- name
- mfg (manufacturer)
- type
- calories
- protein
- fat
- sodium
- fiber
- carbo (carbohydrates)
- sugars
- potas (otasium )
- vitamins
- shelf (display shelf)
- weight
- cups
- rating

## Challenge 1

Get the 5 highest rated cereals. 

- Load the data
- Sort the data on rating
- Get the first five cereals

## Challenge 2 

Create a graph that displays the relative amounts of sugars in each of the top 5 cereals. 

- Use Scale band for your x scale
	- Domain should be: name
- Your y scale should measure carbo
	- Domain is 0 to the max carbo value in the list
	- Range should be the height of your chart

## Challenge 3 

Display an axis at the bottom of the chart. 

- Create a bottom axis that uses the xscale
	- This should display the names of the top five cereals

## Challenge 4 

Display a left axis showing the carbo amount in grams. 

- Create a left axis using your y scale

## Challenge 5

Color the bars in the chart. Create a color scale that gives each cereal a different color. 

- Create an ordinal scale 
- Use name as domain
- Use an array of colors for the range

When completed your chart might look like this: 

![top five cereals](./top-five.png)

## Stretch Challenge 

Further information is needed to develop a product that will disrupt the cereal industry! We need the chemical recipe of the most popular cereal.

The following items are given in grams. Your goal is to display a chart with these values for the most popular cereal. 

- protein
- fat
- fiber
- carbo
- sugars

For the most popular cereal show a graph of the ingredients above. 

To do this make a new array of objects with properties: name and value. The name will be one of the names in the list above. The value will be the value of each property for the most popular cereal. For example: 

```JS
[
	{ name: 'protein', value: 4 },
	{ name: 'fiber', value: 10 }, 
	...
]
```

Next, create a new chart using the new array you created above. 

- Create a new x scale using scale band and the names
- Create a new y scale using scale linear using the values
- Create a new bottom axis
- Create a left axis

When you are complete your chart might look like this: 

![by-grams](./by-grams.png)


