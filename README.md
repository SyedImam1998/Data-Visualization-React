# Data-Visualization-React


### Data Visualization:
- Visualization is suitable when there is a need to argument human capabilities, rather than replace people with computational decision making methods.

### What is D3.js
- D3, or D3.js, stands for Data Driven Documents. It's a JavaScript library for creating dynamic and interactive data visualizations in the browser.

- It is a library for manipulating documents based on data. It allows you to automatically re-render the HTML and SVG elements on your page. It is all about Selection and Data.

- It is kind of similar to JQuery.


```javascript
<div></div>

d3.select('div')
  . selectAll('p')
  .data([1,2,3])
  .enter()
  .append('p')
  .text(dta=>dta);

  // select would select single element 
  // selectAll would select multiple elements
  // data stands for binding data with the selectAll p
  // Now enter will make sure all the p tags have data inside the data and will also have the data if the required amount of p tags are missing example if you see we have 3 elements in the array so there should 3 p tags if they are not found that dat would be available at enter.
  // Now append will make sure they are created
  // text method will set text node inside the p tag
```
### Select Method:
- The select() method selects one element from the document. It takes an argument for the name of the element you want and returns an HTML node for the first element in the document that matches the name.

```javascript
const anchor = d3.select("a");
```
### Append Method:
- The append() method takes an argument for the element you want to add to the document. It appends an HTML node to a selected item, and returns a handle to that node.

### Text Method:
- The text() method either sets the text of the selected node, or gets the current text. To set the value, you pass a string as an argument inside the parentheses of the method.

- It can take a string or a callback function as an argument:

```javascript
d3.select("ul")
  .append("li")
  .text("Very important item");

  // or .text((d)=>d+" USD");
```
### SelectAll:
- D3 also has the selectAll() method to select a group of elements. It returns an array of HTML nodes for all the items in the document that match the input string.

```javascript
const anchors = d3.selectAll("a");
```

### Data Method:
- The data() method is used on a selection of DOM elements to attach the data to those elements. The data set is passed as an argument to the method.

### Enter Method:
- It is used to create a new element for each piece of data present in set.


### Sample Code Explaination:

```html
<body>
  <ul></ul>
  <script>
    const dataset = ["a", "b", "c"];
    d3.select("ul").selectAll("li")
      .data(dataset)
      .enter()
      .append("li")
      .text("New item");
  </script>
</body>
```
It may seem confusing to select elements that don't exist yet. This code is telling D3 to first select the ul on the page. Next, select all list items, which returns an empty selection. Then the data() method reviews the dataset and runs the following code three times, once for each item in the array. The enter() method sees there are no li elements on the page, but it needs 3 (one for each piece of data in dataset). New li elements are appended to the ul and have the text New item.

### Inline Styling:
- D3 lets you add inline CSS styles on dynamic elements with the style() method.

- The style() method takes a comma-separated key-value pair as an argument. Here's an example to set the selection's text color to blue.

```javascript
.style("color","blue");
```

### Change Styles Based on Data:

```javascript
.style('color',(d)=>{
  if(d<20){
    return "red"
  }else{
    return "blue"
  }
})
```

### Add Classes with D3
- Using a lot of inline styles on HTML elements gets hard to manage, even for smaller apps. It's easier to add a class to elements and style that class one time using CSS rules.

#### attr():
- D3 has the attr() method to add any HTML attribute to an element, including a class name.

### SVG:
SVG stands for Scalable Vector Graphics.

Here "scalable" means that, if you zoom in or out on an object, it would not appear pixelated. It scales with the display system, whether it's on a small mobile screen or a large TV monitor.


### How to prepare data:
- Pick up a random data that is is table format.
- Now copy the data into a Google sheet. Clean the data and remove the unnecessary fields. 
- Now download it as an csv file. 
-  Open the downloaded csv file into a notepad and copy the content. 
- Now we need to make this data public so that we can access the data. From our react application. 
- To put this data on public, we'll be using Github Gist.
- Paste the content From the notepad to the Github guest. And publish it. 

#### Github Gist url:
https://gist.githubusercontent.com/SyedImam1998/cd03b2e30b2729312363824c5273a15a/raw/css-named.csv

### Fetch the data from the react:

```javascript
const data=await fetch('https://gist.githubusercontent.com/SyedImam1998/cd03b2e30b2729312363824c5273a15a/raw/css-named.csv');
const csvData=await data.text();
console.log(csvData)
```
#### Difference between using json and text?
- If the data that you receive from the server is adjacent format, then you need to use .json()
- If the data that you receive from the server is not in Json format But other formats like text or csv. Then use .text()

### Parse the data
- The current data that we have got is in text format, but we need in some format that is easily understood by javascript. 
- We can use D3-Dsv This could help us in parsing the data.

```javascript
import "./App.css";
import * as d3 from "d3";
import React, { useState, useEffect } from "react";

export default function App() {
  const getCSVData = async () => {
    try {
      const data = await fetch(
        "https://gist.githubusercontent.com/SyedImam1998/cd03b2e30b2729312363824c5273a15a/raw/css-named.csv",
      );
      const csvData = await data.text();

      // Parse the CSV data using D3
      const parsedData = d3.csvParse(csvData);

      // Now you can work with the parsed data
      console.log(parsedData);
    } catch (error) {
      console.error("Error fetching or parsing CSV data:", error);
    }
  };

  useEffect(() => {
    getCSVData();
  }, []); // Make sure to call the function only once, when the component mounts

  return <main>React ⚛️ + Vite ⚡ + Replit</main>;
}

```

#### Second way to do it (Preferred way):

```javascript
 const getCSVData = async () => {
    try {
      const URL = "https://gist.githubusercontent.com/SyedImam1998/cd03b2e30b2729312363824c5273a15a/raw/css-named.csv";

       d3.csv(URL).then((data) => {
        console.log(data);
      })
  
    } catch (error) {
      console.error("Error fetching or parsing CSV data:", error);
    }
  };
```

### Difference between D3.js And Vega ?
 D3 is more suitable for developers who need fine-grained control and flexibility in creating data visualizations, while Vega is ideal for those who prefer a higher-level abstraction and want to create visualizations quickly and with less code. 