# Data-Visualization-React


### Data Visualization:
- Visualization is suitable when there is a need to argument human capabilities, rather than replace people with computational decision making methods.


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