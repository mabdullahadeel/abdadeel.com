---
author: Abdullah Adeel
pubDatetime: 2021-06-30T15:22:00Z
modDatetime: 2023-12-28T01:10:24Z
title: Reason for developing in GO
slug: reason-for-developing-in-go
featured: true
draft: false
ogImage: ../../assets/blog/reason-for-developing-in-go.png
tags:
  - golang
description: GO is like a hot kid in the market with all the latest features needs to face modern problems in almost every field. The main reason is that GO is a comparatively new language. Programming languages like C & C++ which was developed in 90s could not quite evolve with the modern complexities of the systems. GO solves all of the same problems with much simpler syntax ( which mean less development time) with almost the same performance which leads to the next point.
conicalUrl: https://dev.to/abdadeel/reason-for-developing-in-go-5g0c
---

![reason for developing in go cover image](@assets/blog/reason-for-developing-in-go.png)

## Table of contents

## Introduction

GO also know as [golang](https://golang.org/) is a statically typed and compiled programming language baked by three of the google developers to mainly solve some of google's internal problems. Those three names are **Robert Griesemer**, **Robe Pike**, and **Ken Thompson**. After two years of planning and development, these guys came up with an open-source language in 2009 known as **GO**. At the time of release, GO was only available for macOS and Linux but in few months, windows release also rolled out. Since its release, GO has gained a lot of attention due to its feature pack nature and simple but effective syntax.

Whoops! Let's look at some technical words from the above paragraph and explain them a little bit 😸

<div align="center">
  <img src="https://media.giphy.com/media/hLE84j8EJwMT2aNHHp/giphy.gif">
</div>

## Statically Typed

What is statically typed means?
Statically typed means that the variable we define while writing the program is explicitly declared. Unlike dynamically typed language like `python` where you define the variable like this 👇

```python
name = "abdadeel"
```

In the above example, we don't need to tell the python that we are going to assign a string to the `name` variable.
But In golang, we tell the compiler that this variable that I going to initialize is going to have a string data type store inside it. The syntax is like this👇

```go
var name string = "abdadeel"
// short-hand syntax: go compiler will automatically  infer the type of variable
name := "abdadeel"
```

## Compiled Language

This means that the go compiler first converts all the code to the low-level machine code and then runs that low-level code which is much more efficient and fast ⚡.

<hr>

Below are some of the reasons/characteristics of GO that make it so loveable and why you should also give it a chance.

## 1) Evolved and Ready for Modern Challenges

GO is like a hot kid in the market with all the latest features needs to face modern problems in almost every field. The main reason is that GO is a comparatively new language. Programming languages like C & C++ which was developed in '90s could not quite evolve with the modern complexities of the systems. GO solves all of the same problems with much simpler syntax ( which mean less development time) with almost the same performance which leads to the next point.

## 2) Faster Development

As mentioned earlier, programming languages like C & C++ have complex syntax to write which ultimately leads to harder maintenance and longer development time. GO solves these problems without compromising much on the performance side of things.

## 3) Ease of Programming and Efficiency

Before GO, the developer had to choose one of two given options 👇

- Fast Execution
- Fast Development

But with GO, developers can get the best of both worlds.

## 4) Support for Concurrency & Network Communication

As time passed, computers got more and more powerful to a point where there are virtually multiple working processors in a single processor. This urges developers to write code that can utilize all of those multi-cors and deliver the product that can do things significantly faster utilizing the resources more efficiently. Network communication nowadays has become quite crucial in modern web development so that inter-server communications can be smoother. This is the main reason that GO is loved by the web development community to develop beefy backends.

## 5) Memory Management Support

Go has a built-in memory management system, which takes care of all the problems like `memory leaks`. In older programming languages like C & C++, the developer has to take care of all the memory management, but GO takes that part away by implementing things like [garbage collection](<https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)>) and [reflection capability](https://en.wikipedia.org/wiki/Reflective_programming)

<hr>

# Summary

GO was developed to solve modern problems. It gives the developer ability to write efficient and secure pieces of code in significantly less amount time without sacrificing much of the performance side. GO has been used by big large corporations and tech companies to manage different things serving millions of users per second which proves the abilities of GO. But like every other programming language, GO has its own cons. But I truly believe that you should at least give it a try once. You can try it here 👉 [Open GO playground](https://play.golang.org/p/MAohLsrz7JQ).

Here is the link if you want to get to know the other side of things that why my most favorite tech company ditched `GO` for `RUST` 👇

▶ [Take me to article](https://blog.discord.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f)
