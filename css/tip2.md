---
layout: default
title: Django Fullstack Tips
description: A knowledge-sharing platform
---
# How to create spinner using HTML + CSS

_Pardeep_ <br />
_Jan 21, 2022_

We might need spinner at multiple places in our projects to show some loading or progress. We can create our own spinner using just HTML and CSS

![Spinner](../images/css-tip2-image1.gif)

We will use CSS animation and transition to create this spinner.

**Follow the two simple steps below**

* Create a div element

```
<div id="container">
  <div id="html-spinner"></div>  
</div>
```

* Apply the css to this div element

```
#html-spinner {
  width:50px;
  height:50px;
  margin : 0 auto;
  border:6px solid #0000ff;
  border-top:6px solid #cccccc;
  border-radius:50%;
  transition-property: transform;
  animation: rotate 1.2s linear infinite; 
}

@keyframes rotate {
    from {transform: rotate(0deg);}
    to {transform: rotate(360deg);}
}
```

Let us understand how this spinner is created:

```
transition-property: transform;
animation: rotate 1.2s linear infinite;
```

The *@keyframes* rule specifies the animation code. <br />
We use transition property transform. <br />
We use an animation rule called "rotate". <br />
The animation is created by gradually changing from one set of CSS styles to another using the "from" and "to". <br />
The *animation duration* is of 1.2s. <br />
linear is the *animation-timing-function* that specifies that animation will run with the same speed from start to end. <br />
The *animation-iteration-count* is *infinite*. So, if you want to iterate specific times you can specify an integer. <br />

[Try in CodePen](https://codepen.io/pardeep-thakur/pen/PoJrvBq){:target="\_blank"}.

[back](../)
