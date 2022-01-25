---
layout: default
title: Django Backend Tips
description: A knowledge-sharing platform
---

# Group array of JavaScript objects by duplicate key-value pair/pairs

_Ravi Kumar_  
_Jan 24, 2022_  

This is implementation to group by single/multiple properties in one.

## Implementation

```
const groupBy = (keys,array) =>
    array.reduce((objectsByKeyValue, obj) => {
      const value = keys.map(key => obj[key]).join('-');
      objectsByKeyValue[value] = (objectsByKeyValue[value] || []).concat(obj);
      return objectsByKeyValue;
    }, {});
  
const groupByKeyValue= (groupedArray)=>{
    let answerArray = []
    for (var [key, value] of Object.entries(groupedArray)) {
      value.forEach((arrayElement)=>{
        answerArray.push(arrayElement);
      }) 
    }
    return answerArray;
};
```


## Usage

```
const cars = [
  { brand: 'Peugot', produced: '2021', color: 'yellow' },
  { brand: 'Audi', produced: '2016', color: 'black' },
  { brand: 'Ford', produced: '2016', color: 'red' },
  { brand: 'Audi', produced: '2017', color: 'white' },
  { brand: 'Ford', produced: '2016', color: 'white' },
  { brand: 'Audi', produced: '2016', color: 'green' },
  { brand: 'Peugot', produced: '2018', color: 'white' },
  { brand: 'Ford', produced: '2020', color: 'blue' },
];

const groupByBrand = groupByKeyValue(groupBy(['brand'],cars));
const groupByColor = groupByKeyValue(groupBy(['brand'],cars));
const groupByYear = groupByKeyValue(groupBy(['brand'],cars));
const groupByBrandAndYear = groupByKeyValue(groupBy(['brand','produced'],cars));

console.log("By Brand \n",groupByBrand);
console.log("By Color \n",groupByColor);
console.log("By Year \n",groupByYear);
console.log("By Brand And Year \n",groupByBrandAndYear)
```

### Output
```
By Brand 
 [ { brand: 'Peugot', produced: '2021', color: 'yellow' },
  { brand: 'Peugot', produced: '2018', color: 'white' },
  { brand: 'Audi', produced: '2016', color: 'black' },
  { brand: 'Audi', produced: '2017', color: 'white' },
  { brand: 'Audi', produced: '2016', color: 'green' },
  { brand: 'Ford', produced: '2016', color: 'red' },
  { brand: 'Ford', produced: '2016', color: 'white' },
  { brand: 'Ford', produced: '2020', color: 'blue' } ]
By Color 
 [ { brand: 'Peugot', produced: '2021', color: 'yellow' },
  { brand: 'Audi', produced: '2016', color: 'black' },
  { brand: 'Ford', produced: '2016', color: 'red' },
  { brand: 'Audi', produced: '2017', color: 'white' },
  { brand: 'Ford', produced: '2016', color: 'white' },
  { brand: 'Peugot', produced: '2018', color: 'white' },
  { brand: 'Audi', produced: '2016', color: 'green' },
  { brand: 'Ford', produced: '2020', color: 'blue' } ]
By Year 
 [ { brand: 'Audi', produced: '2016', color: 'black' },
  { brand: 'Ford', produced: '2016', color: 'red' },
  { brand: 'Ford', produced: '2016', color: 'white' },
  { brand: 'Audi', produced: '2016', color: 'green' },
  { brand: 'Audi', produced: '2017', color: 'white' },
  { brand: 'Peugot', produced: '2018', color: 'white' },
  { brand: 'Ford', produced: '2020', color: 'blue' },
  { brand: 'Peugot', produced: '2021', color: 'yellow' } ]
By Brand And Year 
 [ { brand: 'Peugot', produced: '2021', color: 'yellow' },
  { brand: 'Audi', produced: '2016', color: 'black' },
  { brand: 'Audi', produced: '2016', color: 'green' },
  { brand: 'Ford', produced: '2016', color: 'red' },
  { brand: 'Ford', produced: '2016', color: 'white' },
  { brand: 'Audi', produced: '2017', color: 'white' },
  { brand: 'Peugot', produced: '2018', color: 'white' },
  { brand: 'Ford', produced: '2020', color: 'blue' } ]
```