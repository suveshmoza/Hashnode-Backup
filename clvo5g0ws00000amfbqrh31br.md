---
title: "Debouncing and Throttling in JavaScript"
seoTitle: "JS Debounce & Throttle"
seoDescription: "Learn about debouncing and throttling in JavaScript to optimize event handling performance effectively"
datePublished: Wed May 01 2024 18:27:12 GMT+0000 (Coordinated Universal Time)
cuid: clvo5g0ws00000amfbqrh31br
slug: debouncing-and-throttling-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1714587925304/5a49382c-06b7-4834-9d02-9eeb6e866fff.png
tags: js, javascript

---

In the world of web development, responsiveness and performance are crucial aspects that impact user experience. Two techniques often used to optimize performance when handling events like scrolling, resizing, or typing are debouncing and throttling.

### Debouncing

Imagine a scenario where a user is typing in a search bar, and with each keystroke, an API request is sent to get search results. This could result in many requests, possibly overloading the server and creating unnecessary strain. Debouncing addresses this problem by postponing the execution of a function until a set time period passes without any further events occurring.

```javascript
function debounce(func,delay){
    let timeoutId;
    return function(...args){
       clearTimeout(timeoutID);
       timeoutId=setTimeout(()=>{
         func.apply(this,args);
       },delay);
    };
}

const debounceSearch=debounce(searchFunc,1000);
```

In above code, `debounce` takes a function(`func`) and a delay time(`delay`). It returns a new function that when called will execute the func after `delay` miliseconds, resetting the timer each time it is invoked. This ensures that the function is only called after the user has stopped typing for specific duration.

### Throttling

Throttling, similar to debouncing, restricts how often a function can run. But, instead of waiting for a break in events, throttling makes sure the function is called at most once within a set interval.

```javascript
function throttle(func,limit){
    let throttleId;
    return function(...args){
        if(!throttleId){
            func.apply(this,args);
            throttleId=true;
            setTimeout(()=>{
                throttleId=false;
            },limit);
        }    
    };
}

const throttledResize=throttle(resizeHandler,500);
```

In the above code, `throttle` takes a function (`func`) and a time limit (`limit`). It returns a new function that, when called, will run `func` at most once every `limit` milliseconds. If there are more calls during this time, they are ignored until the next interval starts.

### Debouncing vs Throttling

While debouncing and throttling both address the issue of excessive function execution, they serve different purposes and are suitable for different scenarios.

| Debouncing | Throttling |
| --- | --- |
| Debouncing is ideal for scenarios where you want to wait for a pause in events before performing an execution. | Throttling is more suitable for situtations where you want to limit the rate at which a function is called. |