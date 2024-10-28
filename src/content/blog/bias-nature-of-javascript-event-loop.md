---
author: Abdullah Adeel
pubDatetime: 2023-12-11T15:22:00Z
modDatetime: 2024-01-13T20:08:38Z
title: The Bias Nature of JavaScript Event Loop
slug: bias-nature-of-javascript-event-loop
featured: true
draft: false
ogImage: /assets/blog/bias-nature-of-javascript-event-loop.webp
tags:
  - javascript
  - typescript
description: In this article, I'll try to explain most simply; how the event loop handles different tasks assigned to it.
conicalUrl: https://dev.to/abdadeel/the-bias-nature-of-javascript-event-loop-4i9e
---

![The Bias Nature of JavaScript Event Loop | abdadeel](@assets/blog/bias-nature-of-javascript-event-loop.webp)

## Table of contents

## Introduction

JavaScript is the single most controversial language for its single-threaded nature and its bias on handling different tasks assigned to it for execution. In my opinion, the language must not be blamed for it. It could be the requirement of the context in which JavaScript is supposed to run. Yes, it's runtime.

We all know the famous [event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop). In this article, I'll try to explain most simply; how the event loop handles different tasks assigned to it.

In the browser environment, JavaScript despite being a single-threaded language is given multiple tasks (synchronous and asynchronous) to perform. These tasks include rendering the screen including calculating the layouts, applying CSS, and other necessary stuff for efficient rendering of the elements on the screen. It also gives the tasks handling different DOM events like button clicks etc. On top of that, it also needs to execute the code you and I as dev write to make the page interactive and build useable applications. This code could be fetching remote data that the runtime does not even know the execution time of. The poor language has to handle everything in parallel while maintaining a smooth user experience. The language handles all this by leveraging mainly two things:

- Task Prioritization (via callback queues)
- Web APIs

_In the case of NodeJS, WebAPIs are replaced by C++ APIs and the same goes for other newer runtimes._

The main focus of this article is to elaborate on **Task Prioritization** and how the event loop handles different task queues. There are mainly the following queues:

- Micro-Tasks queue
- Macro-Tasks queue
- Animation callback queue

## Micro-Tasks

Microtasks are tasks with higher priority, typically involving promises
(`Promise.resolve`), `process.nextTick` (Node specific), and `MutationObserver`. When a microtask is added to the queue during the execution phase, it will be executed before the next rendering, I/O, or timer task. Since the micro-tasks are of the highest priority, the event loop will start processing micro-tasks as soon as callstack is available empty and keep processing tasks/callbacks in the micro-tasks queue until there are none left.
Here is a simple flow of event loop processing micro-tasks as soon as callstack is empty.

![javascript event loop handling micro-tasks](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7mmr5t4k78zteok8789k.png)

In other words, once the micro-tasks queue claims execution, the event loop will keep processing tasks in the queue as long as there are tasks available before moving ahead. Thus, micro-tasks are the event loop's highest priority.

## Macro-Tasks

Macro-tasks include tasks like setTimeout, setInterval, I/O operations, and UI rendering. These tasks have a lower priority than microtasks. When the call stack is empty, the event loop picks up the next macro-task from the queue and executes it. The primary difference is that not all tasks are picked up for execution once the execution context is given to the macro-tasks queue. Only the first one in the queue is picked up and executed. And event loop moves back to handling other potentially more important tasks like micro-tasks. Here is a simple flow demonstration.

![Javascript event loop handling macro-tasks](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wr320h3evqqjp2xmvbp9.png)

## Animation callbacks

The animation callback queue in browser environments plays a pivotal role in orchestrating smooth and synchronized animations on web pages. Specifically tied to the requestAnimationFrame() method, this queue handles tasks related to rendering updates and animations. When `requestAnimationFrame()` is utilized to schedule animation tasks, these callbacks are placed in the animation callback queue. These tasks are then executed before the subsequent repaint of the browser's display (as per web standards).
The number of tasks going to be processed in one iteration of the event loop depends on the number of tasks available in the animation callback queue at the time of starting the execution of animation callbacks. Any task added to the animation callbacks queue will be processed in the next iteration. Here is a simple demonstration.

![Javascript event loop handling animation callback queued tasks.](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kxcshfn9klublvpuwtxx.png)

So, there's not a single callback queue where the callbacks are queues to be executed by the event loop but a group of queues with different priorities. Event loop process callbacks based on the queue's priority. Thus, the event loop is biased towards some tasks that are of higher importance than others.
