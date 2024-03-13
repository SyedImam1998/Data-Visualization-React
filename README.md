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

- Here "scalable" means that, if you zoom in or out on an object, it would not appear pixelated. It scales with the display system, whether it's on a small mobile screen or a large TV monitor.
- SVG shapes for a web page must go within an HTML svg tag.
- CSS can be scalable when styles use relative units (such as vh, vw, or percentages), but using SVG is more flexible to build data visualizations.

```html
<svg></svg>
```
### Display Shapes with SVG

- There are a number of supported shapes in SVG, such as rectangles and circles. They are used to display data. For example, a rectangle (<rect>) SVG shape could create a bar in a bar chart.
- When you place a shape into the svg area, you can specify where it goes with x and y coordinates. The origin point of (0, 0) is in the upper-left corner. Positive values for x push the shape to the right, and positive values for y push the shape down from the origin point.
- An SVG rect has four attributes. There are the x and y coordinates for where it is placed in the svg area. It also has a height and width to specify the size.
 

### Invert SVG Elements

In SVG, the origin point for the coordinates is in the upper-left corner. An x coordinate of 0 places a shape on the left edge of the SVG area. A y coordinate of 0 places a shape on the top edge of the SVG area. Higher x values push the rectangle to the right. Higher y values push the rectangle down.

To make the bars right-side-up, you need to change the way the y coordinate is calculated. It needs to account for both the height of the bar and the total height of the SVG area.

The height of the SVG area is 100. If you have a data point of 0 in the set, you would want the bar to start at the bottom of the SVG area (not the top). To do this, the y coordinate needs a value of 100. If the data point value were 1, you would start with a y coordinate of 100 to set the bar at the bottom. Then you need to account for the height of the bar of 1, so the final y coordinate would be 99.

The y coordinate that is `  y = heightOfSVG - heightOfBar ` would place the bars right-side-up.

Change the callback function for the y attribute to set the bars right-side-up. Remember that the height of the bar is 3 times the data value d.

Note: In general, the relationship is `y = h - m * d`, where m is the constant that scales the data points.

###  Linear Scale with D3
- The bar and scatter plot charts both plotted data directly onto the SVG. However, if the height of a bar or one of the data points were larger than the SVG height or width values, it would go outside the SVG area.
- In D3, there are scales to help plot data. scales are functions that tell the program how to map a set of raw data points onto the pixels of the SVG.
- For example, say you have a 100x500-sized SVG and you want to plot Gross Domestic Product (GDP) for a number of countries. The set of numbers would be in the billion or trillion-dollar range. You provide D3 a type of scale to tell it how to place the large GDP values into that 100x500-sized area.
- D3 has several scale types. For a linear scale (usually used with quantitative data), there is the D3 method scaleLinear():

```javascript
const scale = d3.scaleLinear()
```
- By default, scales use the identity relationship. This means the input value maps to the output value. However, scales can be much more flexible and interesting.

#### Domain
- Say a dataset has values ranging from 50 to 480. This is the input information for a scale, also known as the domain.
#### Range

- You want to map those points along the x axis on the SVG, between 10 units and 500 units. This is the output information, also known as the range.

The domain() and range() methods set these values for the scale. Both methods take an array of at least two elements as an argument. Here's an example:

### Min and Max:
- The D3 methods domain() and range() set that information for your scale based on the data. There are a couple methods to make that easier.

- Often when you set the domain, you'll want to use the minimum and maximum values within the data set. Trying to find these values manually, especially in a large data set, may cause errors.

```javascript
const exampleData = [34, 234, 73, 90, 6, 52];
d3.min(exampleData)  // 6
d3.max(exampleData) // 234
```

#### Nested Array:

```javascript
const locationData = [[1, 7],[6, 3],[8, 3]];
const minX = d3.min(locationData, (d) => d[0]);
// output 1
```

### Add Axes to a Visualization
- Another way to improve the scatter plot is to add an x-axis and a y-axis.

- D3 has two methods, axisLeft() and axisBottom(), to render the y-axis and x-axis, respectively. Here's an example to create the x-axis based on the xScale in the previous challenges:

```javascript
const xAxis = d3.axisBottom(xScale);
```

### DOMContentLoaded
- When you want to run the certain functions only after the DOM has fully rendered.

```javascript
document.addEventListener('DOMContentLoaded', function(){})
```
### Get JSON with the JavaScript XMLHttpRequest Method

- You can also request data from an external source. This is where APIs come into play.

- Remember that APIs - or Application Programming Interfaces - are tools that computers use to communicate with one another. You'll learn how to update HTML with the data we get from APIs using a technology called AJAX.

- Most web APIs transfer data in a format called JSON. JSON stands for JavaScript Object Notation.

- JSON syntax looks very similar to JavaScript object literal notation. JSON has object properties and their current values, sandwiched between a { and a }.

- These properties and their values are often referred to as "key-value pairs".

- However, JSON transmitted by APIs are sent as bytes, and your application receives it as a string. These can be converted into JavaScript objects, but they are not JavaScript objects by default. The JSON.parse method parses the string and constructs the JavaScript object described by it.

- You can request the JSON from freeCodeCamp's Cat Photo API. Here's the code you can put in your click event to do this:


```javascript
const req = new XMLHttpRequest();
req.open("GET",'/json/cats.json',true);
req.send();
req.onload = function(){
  const json = JSON.parse(req.responseText);
  document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
};
```
- Here's a review of what each piece is doing. The JavaScript XMLHttpRequest object has a number of properties and methods that are used to transfer data. 
- First, an instance of the XMLHttpRequest object is created and saved in the req variable. Next, the open method initializes a request - this example is requesting data from an API, therefore is a GET request.
 - The second argument for open is the URL of the API you are requesting data from. The third argument is a Boolean value where true makes it an asynchronous request. The send method sends the request. 
 - Finally, the onload event handler parses the returned data and applies the JSON.stringify method to convert the JavaScript object into a string. This string is then inserted as the message text.
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