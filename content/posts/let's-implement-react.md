+++
title = "Let's implement React"
featured_image = "/invoker.jpg"
featured_image_class = "cover bg-top"
date = '2026-07-04T11:24:51+05:00'
draft = false
+++

## Introduction

Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ratione id necessitatibus quis! Iure accusantium consequuntur possimus excepturi. Sequi et dolor nisi autem? Ut est vero quae aliquid suscipit, molestias reprehenderit?
Numquam fuga ea iste, veniam officiis molestias repellat alias, culpa a excepturi sit magni facere fugit cupiditate eius vel. Vero dignissimos perferendis expedita eligendi. Quod officia maiores consequatur sit obcaecati!

Observer

```js
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

## Section 2

Lorem ipsum, dolor sit amet consectetur adipisicing elit. Illo nulla, consequatur iure a enim necessitatibus facilis amet temporibus dolorum atque animi, fuga minus eos ea aperiam facere reiciendis in? Maiores.
Inventore, consequatur sapiente fugiat hic facere voluptatibus expedita praesentium doloremque numquam, tenetur, tempora quae id voluptate excepturi debitis molestiae atque ipsa? Odit a sint fugit vero repudiandae iure minima eos.
Blanditiis, minus iste fugiat ipsa dolores labore saepe odit quaerat unde laborum porro officiis expedita iusto nihil possimus odio aliquid ratione omnis mollitia. Accusamus, veniam. Ab iste corporis commodi temporibus!

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

## Section 3

Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed, rerum ipsa nisi earum ratione natus cum iste beatae quasi aut laudantium harum sint tempora perspiciatis? Similique fuga natus consequatur quaerat!
Voluptas deserunt atque ab deleniti hic exercitationem repellat? Pariatur explicabo eaque commodi magnam possimus placeat voluptate in quam. Inventore, nobis aliquam minima et repudiandae excepturi id fugit beatae libero consequatur?
Ipsa minus quae sed eos consectetur, atque possimus ad, quaerat soluta pariatur exercitationem cumque in repellat repellendus, maxime excepturi cupiditate aliquam consequatur labore praesentium non ratione quam. Voluptate, delectus eius!

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

## Overview

Lorem ipsum, dolor sit amet consectetur adipisicing elit. Veritatis consequatur quidem ut reiciendis error? Minus officia dolores eveniet! Repudiandae ullam placeat itaque nihil sunt impedit soluta pariatur earum quos molestias!

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
