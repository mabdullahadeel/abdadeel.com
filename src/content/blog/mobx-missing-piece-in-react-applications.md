---
author: Abdullah Adeel
pubDatetime: 2023-03-16T15:22:00Z
modDatetime: 2024-01-13T20:01:38Z
title: MobX  -  The missing piece in your complex react applications
slug: mobx-missing-piece-in-react-applications
featured: true
draft: false
ogImage: /assets/blog/mobx-missing-piece-in-react-applications.webp
tags:
  - react
  - mobx
description: In this article, I'll show you how to use MobX to manage state in your complex react applications.
conicalUrl: https://dev.to/abdadeel/mobx-the-missing-piece-in-your-complex-react-applications-5320
---

![MobX  -  The missing piece in your complex react applications | abdadeel](@assets/blog/mobx-missing-piece-in-react-applications.webp)

## Table of contents

## Introduction

I have always been a big fan of simplicity when managing global state in front-end applications. For a long time, redux has dominated this space and it still is a good option for most applications. But recently we’ve started seeing intuitive, lightweight, and generally better ways of handling global state. The most prominent libraries are **zustand, jotai, recoil,** and a few others.

This article is not aimed to convince you to use `mobx` in all of your react applications but how you should plan the architecture with the right tool to manage the global state given the nature of your application.

MobX is not React’s state management library but a Javascript state management library and can work well with a variety of frameworks and react is just one of them. At its core, it uses the concept of “**observables”**. An observable is a special type of object that notifies its so-called subscribers when its value changes. These subscribers can listen to the changes from the observable and react to those changes if they feel like it. In case of `react`, those subscribers are React components that trigger re-render when the value of observable changes. Other features provided by the`mobx` include actions, computed, and reactions. We won’t go into details about the primitives of `mobx` but you are free to learn more about them in the documentation [here](https://mobx.js.org/README.html).

As mentioned earlier, `mobx` is a state management library for javascript not for react. So, to make it work with react, a separate set of utilities is required. That is provided by **mobx-react-lite.** (There is a separate “mobx-react” package but for most applications, the lite version has everything covered).

The most prominent feature of `mobx` that makes it unique and the best choice for complex applications is managing state using classes. That opens doors to using your favorite design patterns in your fronted application while keeping the UI in sync. Combined with fine-grained reactivity, it becomes a perfect tool for building complex front-end applications.

Let’s build a simple spreadsheet application logic to understand the basic concepts of `mobx`.

As mentioned earlier, there are four primary primitives exposed by `mobx`.

- [**_observable_**](https://mobx.js.org/observable-state.html)**_:_** This creates a basic observable value that can be observed by reactive functions and components. When the value changes, any reactive functions that depend on it will be re-run.
- [**_action_**](https://mobx.js.org/actions.html)**_:_** an action is a function that modifies the state of observables in a predictable and controlled way. Actions are used to encapsulate state mutations and ensure that they are performed in a consistent way so that MobX can properly track the changes and update any dependent observables.
- [**_computed_**](https://mobx.js.org/computeds.html): This creates a computed value that depends on one or more observable values. When any of the observable values change, the computed value will be re-computed automatically.
- [**_reaction_**](https://mobx.js.org/reactions.html): This creates a reactive function that will be automatically re-run whenever a specific observable value changes.

This example takes the class-based approach but you can go through the docs to know about other handy approaches that allow you to basically get the same results. So in the end, it’s your decision that should only be affected by the application requirements.

Now, let’s start with our simple spreadsheet application.

```typescript
// file: store.ts
import { makeObservable, observable, action, computed } from "mobx";

class SpreadsheetStore {
  data: number[][] = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
  ];

  constructor() {
    makeObservable(this, {
      data: observable,
      updateCell: action,
      rowCount: computed,
      columnCount: computed,
      cellData: computed,
    });
  }

  get rowCount(): number {
    return this.data.length;
  }

  get columnCount(): number {
    return this.data[0].length;
  }

  updateCell(rowIndex: number, columnIndex: number, value: number) {
    this.data[rowIndex][columnIndex] = value;
  }
}

export const store = new SpreadsheetStore();

// Example usage:
store.updateCell(0, 0, 10);
console.log(store.data);
```

`makeObservable` is a MobX utility function that allows you to define observable states, actions, and computed properties on an object which in this case is a class instance but can be a plain object or any primitive.

In this case, we pass the `this` object (which refers to the current `SpreadsheetStore` instance) as the first argument to `makeObservable`. We then pass a descriptor object as the second argument, which defines the observables, actions, and computed properties of the class.

But, mapping class members to `mobx` primitives can be tedious sometimes. That is where `makeAutoObservable` comes in handy. `makeAutoObservable` is a simpler way to define observables, actions, and computed properties on a class. It automatically detects and creates observables for any property that is accessed or modified during the construction of the object, and also detects and creates actions for any method that modifies observables.

```typescript
// file: store.ts
import { makeAutoObservable } from "mobx";

class SpreadsheetStore {
  data = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
  ];

  constructor() {
    makeAutoObservable(this);
  }

  updateCell(rowIndex, columnIndex, value) {
    this.data[rowIndex][columnIndex] = value;
  }

  get rowCount() {
    return this.data.length;
  }

  get columnCount() {
    return this.data[0].length;
  }
}

export const store = new SpreadsheetStore();

// Example usage:
store.updateCell(0, 0, 10);
console.log(store.data);
```

In this case, `getters` are automatically mapped as computed, while methods are actions by default. Any property is observable. This is short and concise but comes with [limitations](https://mobx.js.org/observable-state.html#limitations).

Now that we’ve state, let’s consume that in react component.

```tsx
import React from "react";
import { observer } from "mobx-react-lite";
import store from "./store";

const Spreadsheet: React.FC = observer(() => {
  const handleCellChange = (
    event: React.ChangeEvent<HTMLInputElement>,
    rowIndex: number,
    columnIndex: number
  ) => {
    const newValue = parseInt(event.target.value);
    store.updateCell(rowIndex, columnIndex, newValue);
  };

  return (
    <div>
      <table>
        <tbody>
          {store.data.map((row, rowIndex) => (
            <tr key={rowIndex}>
              {row.map((cell, columnIndex) => (
                <td key={columnIndex}>
                  <input
                    type="number"
                    value={cell}
                    onChange={event =>
                      handleCellChange(event, rowIndex, columnIndex)
                    }
                  />
                </td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
});

export default Spreadsheet;
```

Here, `observer` [HOC](https://reactjs.org/docs/higher-order-components.html) is imported from `mobx-react-lite` the package which makes `Spreadsheet` component react to the changes. The cool part here is that you don’t manually have to use selectors to select just that state that you want to avoid unnecessary re-renders. `mobx` handles that for you.

That wraps up this introductory example. Mobx has a special place when it comes to global state management libraries. You might not need it for your simple e-commerce site or a simple CMS site. You can easily get away with something like **zustand** or **jotai** which are more lightweight and easy to use than `mobx` . But when you’ve complex use cases where there are dependent states and application logic heavy, you should consider using`mobx` .
