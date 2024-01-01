---
author: Abdullah Adeel
pubDatetime: 2021-06-30T15:22:00Z
modDatetime: 2024-01-01T19:20:05Z
title: Basic Data Types in GO
slug: basic-data-types-in-go
featured: true
draft: false
ogImage: ../../assets/blog/basic-data-types-in-go.jpg
tags:
  - golang
description:
  GO has all the basic and advanced data types like other programming languages.
  Before we dive into the data types, let's first have a look at some conventions in GO.
conicalUrl: https://dev.to/abdadeel/all-basic-data-types-in-go-55n8
---

![Basic data types in golang](@assets/blog/basic-data-types-in-go.jpg)

## Table of contents

## Introduction

GO has all the basic and advanced data types like other programming languages. Before we dive into the data types, let's first have a look at some conventions in GO.

![are-you-ready](https://media.giphy.com/media/hTBkgmCL1g79DUvAiR/giphy.gif)

## Filenames in GO

GO code is written and stored in the `.go` file. The filename itself can consist of `lower-case` letters by convention. For example `codewithab.go` is a valid filename by convention. In another case, if file names have multiple words, that word should be separated by `_` rather than camel case by convention. Like `code_with_ab.go` is a valid file name in that case. The main constraints in the filename that cause the filename to be invalid are 👇:

    - Including spaces in the filename
    - Including special characters like `@`, `#`, `$`

## Identifiers in GO

**_Identifiers_** are the elements of a program (go program) that are assigned by the user/developer like a variable is defined by the developer. The same is the case for a `function` name.
Below are some examples of **NOT** valid identifiers 👇

- `1codewithab` -> `INVALID` (Reason❓: identifier name cannot start with a `number`)
- `for` -> `INVALID` (Reason❓: `for` is a special/reserved keyword in GO use to define `for-loops` ) </br> If you want to read about all the `GO` reserved words, you can have a brief look at them [here](https://medium.com/wesionary-team/know-about-25-keywords-in-go-eca109855d4d) 👈
- `code+with+ab` -> `INVALID` (Reason❓: identifier name connot contain special characters)
- `code_with_ab` -> `VALID`

<hr>

# Go Data Types

In this article, we will focus and discuss the details about these data types 👇

- [Strings](#string)
- [Boolean](#bool)
- Integers
  - [int8](#intergers)
  - [int16](#intergers)
  - [int32](#intergers)
  - [int64](#intergers)
  - [uint8](#intergers-u)
  - [uint16](#intergers-u)
  - [uint32](#intergers-u)
  - [uint64](#intergers-u)
  - [uintptr](#intergers-u)
- [Complex Numbers](complex)

<div id="string"></div>
# Strings
String type in GO is basically a slice of `bytes` type. But here is the interesting fact about this type. GO in fact does not have any `byte type` but the `byte` type is an alias for the `uint8` type. Pretty confusing right 😵?

![mind-boggling](https://media.giphy.com/media/7FgDseZw8Zw9Gi0OMk/giphy.gif)

Okay, so let's simplify it. In short, the `string` type is basically a collection of `byte` types where each character of the string is represented separately.

```go
package main

import (
    "fmt"
)

func printIndividialBytes(fullString string) {
    fmt.Printf("Bytes: ")
    for i := 0; i < len(fullString); i++ {
        fmt.Printf("%x ", fullString[i])
    }
}

func main() {
    name := "Code with AB"
    fmt.Printf("String: %s\n", name)
    printIndividialBytes(name)
}

/* Output: 👇
String: Code with AB
Bytes: 43 6f 64 65 20 77 69 74 68 20 41 42
*/
```

[Run In Playground 🔗](https://play.golang.org/p/LJV2uawhtLn)

<div id="bool"></div>
# Boolean
Boolean is the same as pretty much any other programming language with `true` and `false` as options.

```go
var isPaidCustomer bool = true;
```

<h1> Integers Type </h1>

Integer types are differed by the memory allocation of the particular variable. To make it more clear. Let's take an example.
Let's define a variable and initialize it with a number and a data type of `int8`.

```go
var years_of_coding int8 = 3;
```

In the above example, the variable `years_of_coding` will take `8 bits` of space on memory.

Similarly

<div id="intergers">
- int8 -> `-128 to 127 bits`
- int16 -> `-32768 to 32767`
- int32 -> `− 2,147,483,648 to 2,147,483,647`
- int64 -> `− 9,223,372,036,854,775,808 to 9,223,372,036,854,775,807`

<div id="intergers-u"></div>
### For unsigned integers

- uint8 -> `0 to 255`
- uint16 -> `0 to 65,535`
- uint32 -> `0 to 4,294,967,295`
- uint64 -> `0 to 18,446,744,073,709,551,615`

For unsigned integers, GO documentation clearly says this 👇

> The int, uint, and uintptr types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems. When you need an integer value you should use int unless you have a specific reason to use a sized or unsigned integer type.

<div id="complex"></div>
Complex numbers are supported by GO. They have the following form 👇:
```go
re + img¡
```
where `re` is the `real` part of the complex number and `img` is the `imaginary` part of the complex number.

```go
package main
import "fmt"

func main(){
    // To declare complex number (real +imaginary(¡))
    var comp complex64 = 5 + 10i
    fmt.Printf("The value is: %v", comp)
}
/*
OUTPUT 👇
The value is: (5+10i)
*/
```

`%v` is used to print the `formatted` complex number.
To print `real` and `imaginary` parts as separate use `%f`

<hr>

That's it from my side for today. I hope you learn something today. If you want to practice along with that I would highly encourage, you can visit the playground [here](https://play.golang.org/).
