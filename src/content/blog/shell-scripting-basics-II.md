---
author: Abdullah Adeel
pubDatetime: 2022-01-03T15:22:00Z
modDatetime: 2024-01-01T19:20:05Z
title: Shell Scripting Basics - Beginner's Guide - Part II
slug: shell-scripting-basics-part-2
featured: true
draft: false
ogImage: /assets/blog/shell-scripting-basics-II.webp
tags:
  - shell
  - bash
description:
  Part II - Shell scripting is the code that is designed to run in the Unix shell.
  This means that you can write these generic pieces of instructions and execute
  them directly from the shell on Linux and MacOS.
conicalUrl: https://dev.to/abdadeel/shell-scripting-basics-beginners-guide-part-ii-4cfo
---

![Shell scripting basics - Beginner's guide | abdadeel](@assets/blog/shell-scripting-basics-II.webp)

## Table of contents

## Introduction

In my [last post](https://abdadeel.com/posts/shell-scripting-basics) about shell scripting, I talked about the basics of shell scripting. In this article, I am going to discuss some unfamous commands/uses of shell scripting extending the previous ones.

If you're a complete beginner to shell scripting, you should still be able to get everything in this article but it is recommended that you first read [this](https://abdadeel.com/posts/shell-scripting-basics) and join me back here. I'll be waiting.

![waiting](https://media.giphy.com/media/QBd2kLB5qDmysEXre9/giphy.gif)

<hr>

## Referencing the script itself

In your shell script flow, there may be some scenarios where you need to access the information about the currently running script. Let's say you want to know the name of the script currently being executed at the time of execution. You can simply do that by using `$0`. You might have seen this syntax in the previous article. In that case, you could use similar syntax to access the flags/argument passed to the script when executing. But in this case `$0` is just the reference to the current script.

```bash
#! /bin/bash

echo "The name of the current file is $0"
```

## Declaring an Array

Arrays are one of the most commonly used data structures out there and bash also supports arrays with pretty much straightforward syntax.
An array can be initialized using `( )` and you can pass default values separated by spaces. A simple example is shown below.

```bash
#! /bin/bash/

my_friends=("Aley" "John" "Doe")

```

To access the values stored in an array, you can simply use the index to access the value. Keep in mind that indexes start from `0`.

```bash
#! /bin/bash

echo ${my_friends[0]}

: '
Output:
>> Aley
'

```

Similarly, the negative index can be used to access the value from the end of the array.

```bash
#! /bin/bash

echo ${my_friends[-1]}

: '
Output:
>> Doe
'

```

## Until Loop

Until loops work similarly to while loops with the only difference being it on terminate when the condition returns `True`.

```bash
until [ your_condition ]
do
        <some_command>
done

```

A great use case of until would be waiting for the database to be available before starting the main server to prevent crashes.

```bash
#! /bin/bash

postgres_ready() {
python << END
import sys
import psycopg2
try:
    psycopg2.connect(
        dbname="${POSTGRES_DB}",
        user="${POSTGRES_USER}",
        password="${POSTGRES_PASSWORD}",
        host="${POSTGRES_HOST}",
        port="${POSTGRES_PORT}",
    )
except psycopg2.OperationalError:
    sys.exit(-1)
sys.exit(0)
END
}
until postgres_ready; do
  >&2 echo 'Waiting for PostgreSQL to become available...'
  sleep 1
done
>&2 echo 'PostgreSQL is available'

: '
# src 👇
https://bit.ly/3nlrS2q
'
```

At this point, you're ready to take charge of handling automated shell scripts in your team workflow.
For more web dev content and resources, please join [my Twitter](https://twitter.com/abdadeel_) family by following [@abdadeel\_](https://twitter.com/abdadeel_).
