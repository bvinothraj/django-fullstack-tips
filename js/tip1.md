---
layout: default
title: Django Fullstack Tips
description: A knowledge-sharing platform
---

# How to check execution time of a code block

_B Vinoth Raj_   
_Jan 20, 2022_  
  
During development you may oftentimes come across the need to check execution time for a code block.  
  
Two console functions make this job easy:  
```
console.time("some label")  
// some code
console.timeEnd("some label")  
```

The following example illustrates:
```
console.time("time taken");

var arr = new Array(1000),
    len = arr.length,
    i;

for (i = 0; i < len; i++) {
    arr[i] = new Object();
};

console.timeEnd("time taken"); 

// Example output:
time taken: 0.178955078125 ms

```

[back](../)
