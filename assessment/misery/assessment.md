# ACS 4310 Final Assessment: What Makes a Country Miserable?

You've just been hired as a data analyst at a global aid organization. They have a limited budget and need to decide where to send help first. Your manager hands you a spreadsheet and says:

> "This file scores almost every country on earth on how badly things are going. I need to see which countries are in the most trouble — and I need to know what 'trouble' actually looks like in the numbers. Have something on screen by the end of the day."

Your dataset is `Gross Domestic Misery - World Data - World Data.csv` in this folder. Copy it into your working folder and rename it `misery.csv` to make it easier to load.

It has 186 countries and these fields:

| Field | What it means |
|:------|:--------------|
| `COUNTRY` | Country name |
| `Fragile States Index` | How close a country is to collapse. **Higher = more fragile** |
| `Women, Peace, and Security Index` | Women's inclusion, justice, and safety. 0–1, **higher = better** |
| `Poverty Rate(2010-2020)` | % of people living in poverty |
| `Infant Mortality` | Babies who die before age 1, per 1,000 births |
| `Unemployment Rate(2000-2020)` | % of workers without jobs |
| `Violent Crime Index Rate(2022)` | Violent crime rate |
| `Suicide Rate(2022)` | Suicides per 100,000 people |
| `Incarceration Rate(2022)` | Prisoners per 100,000 people |
| `Global Rate Depression(2022)` | % of people with depression |
| `Global Alcoholism rate(2019)` | % of people with alcohol use disorder |
| `Global Drug Rate(2019)` | % of people with drug use disorder |

You'll use D3, SVG, scales, and axes — the same tools from your three visualizations. Look back at your own code and the [D3 tutorial](https://github.com/Tech-at-DU/d3-tutorial) as much as you like.

**Heads up:** this is real-world data, and real-world data is messy. Some cells are empty. Part of the job is noticing that.

Each challenge ends with a **Question**. Write your answers in a `README.md` next to your code — one or two sentences each is plenty. The answers matter as much as the charts.

---

## Part 1: Load and clean (≈15 min)

### Challenge 1

Set up an HTML page with:

- A heading: "What Makes a Country Miserable?"
- Your name underneath
- Two `<svg>` elements, one for each chart you'll build
- A `<script>` tag that loads D3, and a `<script>` tag for your own code

### Challenge 2

Load `misery.csv` with `d3.csv()` and log the result.

Every value comes in as a **string**, and empty cells come in as `""`. Use the row conversion function to turn the fields you need into numbers. Empty cells should become `null`, not `0` — a missing value is not the same as zero!

```JS
const num = (value) => value === '' ? null : Number(value)

const data = await d3.csv('misery.csv', d => ({
  country: d.COUNTRY,
  fragility: num(d['Fragile States Index']),
  // add the other fields you need here
}))
```

Log the data again and check that the numbers are numbers.

**Question 1:** How many countries are in the dataset? How many are missing a Fragile States Index score?

---

## Part 2: Who is in the most trouble? (≈30 min)

### Challenge 3

Find the **10 most fragile countries**.

- Filter out countries where `fragility` is `null`
- Sort from highest to lowest `fragility`
- Keep the first 10

Log them to the console.

### Challenge 4

Draw a bar chart of those 10 countries in your first `<svg>`.

- **x scale:** `d3.scaleBand()`, domain is the country names
- **y scale:** `d3.scaleLinear()`, domain is `0` to the max fragility
- Draw one `<rect>` per country

### Challenge 5

Add axes and labels.

- A bottom axis showing country names (rotate the labels if they overlap)
- A left axis showing the fragility score
- A text label on the y axis: "Fragile States Index"

**Question 2:** Look at your chart. One country does not look like the others. Which one, and by how much? Do you think this is real, or could it be a problem with the data? How would you find out?

### Challenge 6

Now find the **10 least fragile countries** — the most stable places on earth — and log them.

Careful! Try sorting *without* filtering out the `null` values first and see what you get.

**Question 3:** Which country is the least fragile? (If you remember the happiness assessment, does this ring a bell?) What happened when you forgot to filter the empty values?

---

## Part 3: What does "trouble" look like? (≈30 min)

A bar chart shows *who*. A scatter plot shows *why*. Each dot will be one country.

### Challenge 7

In your second `<svg>`, draw a scatter plot:

- **x:** `fragility`
- **y:** `infantMortality`
- Use `d3.scaleLinear()` for both, with `d3.extent()` or `d3.max()` for the domains
- Only plot countries that have **both** values (filter out the `null`s)
- Draw one `<circle>` per country, `r` about 4, with some transparency (`opacity: 0.6`)
- Add a bottom axis, a left axis, and a label for each

### Challenge 8

Add a **trend line** using linear regression from [lesson 14](../../lessons/lesson-14.md).

- Calculate the slope and intercept
- Use them to find the y value at the smallest and largest x
- Draw it with `d3.line()` in a color that stands out from the dots

**Question 4:** Which way does the line go? In plain English, what does that tell your manager about fragile countries and their babies?

### Challenge 9: Predict, then plot

**Before you write any code**, write down your prediction in your README:

> "In more fragile countries, I think depression rates will be **higher / lower / about the same**, because ___."

Now change your scatter plot's y value to `depression` (`Global Rate Depression(2022)`). Update the y scale, the y axis, the y label, and the trend line.

**Question 5:** Was your prediction right? Look at which countries have the *highest* depression rates. Why might the data show this? *Hint: think about what has to happen before a person gets counted as "depressed" in a dataset.*

This is the most important lesson in data visualization: **a chart shows what was measured, not always what is true.** Being able to say that out loud is what separates a data analyst from someone who makes charts.

---

## Stretch Challenges

Finished early? Pick any of these.

### Stretch 1: Tooltips

Add a tooltip to the scatter plot that shows the country name and both values on hover (see [lesson 15](../../lessons/lesson-15.md)). Use it to find out which country sits *furthest* from the trend line.

### Stretch 2: Pick your own y

Add a `<select>` dropdown listing every numeric field. When the user picks one, redraw the scatter plot (dots, y axis, label, trend line) against `fragility`. Use a transition so the dots slide to their new positions.

**Question:** Which field has the *strongest* relationship with fragility? Which has almost none?

### Stretch 3: Where do you live?

Highlight your own country (or one you care about) in both charts with a different color and a text label. Where does it land?

### Stretch 4: Sort it

Add a button to the bar chart that toggles between the 10 most fragile and the 10 least fragile countries, animating the bars between them.

---

## Submit

- Your `index.html`, your JavaScript, and `misery.csv`
- Your `README.md` with answers to Questions 1–5 and your Challenge 9 prediction
- Make sure the page runs with **no console errors**
