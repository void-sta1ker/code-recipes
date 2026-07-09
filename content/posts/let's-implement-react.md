+++
title = "Let's implement React"
featured_image = "/invoker.jpg"
featured_image_class = "cover bg-top"
date = '2026-07-04T11:24:51+05:00'
draft = false
+++

## Introduction

Observer
```js {class="mb2"}
const subscribers = []; // also called observers or listeners

function subscribe(subscriber) {
  subscribers.push(subscriber);
}

function unsubscribe(subscriber) {
  const index = subscribers.indexOf(subscriber);
  if (index !== -1) {
    subscribers.splice(index, 1);
  }
}
```
<!--more-->
useState.js
```js
let state;

function dispatcher(newValue) {
  state = newValue;
  subscribers.forEach((subscriber) => subscriber());
}

exports.useState = function useState(initialValue) {
  if (!state) {
    state = initialValue;
  }

  if (!subscribers.includes(useState.caller)) {
    subscribe(useState.caller);
  }

  return [state, dispatcher];
};
```

useEffect.js
```js
let ref;

exports.useEffect = function useEffect(callback, deps = []) {
  if (!subscribers.includes(useEffect.caller)) {
    subscribe(useEffect.caller);
  }

  if (ref === undefined) {
    ref = [...deps];
    callback();
    return;
  }

  deps.forEach((dep, index) => {
    const refItem = ref[index];

    if (refItem !== dep) {
      ref[index] = dep;
      callback();
    }
  });
};
```

Client code
```js
const { useState } = require("./useState.js");
const { useEffect } = require("./useEffect.js");

function Main() {
  const [count, setCount] = useState(0);

  const timeoutId = setTimeout(() => {
    setCount(count + 1);
    clearTimeout(timeoutId);
  }, 1000);

  useEffect(() => {
    console.log("useEffect: ", count);
  }, [count]);
}

Main();
```
