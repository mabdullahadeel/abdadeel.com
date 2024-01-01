---
author: Abdullah Adeel
pubDatetime: 2021-10-23T15:22:00Z
modDatetime: 2024-01-01T19:20:05Z
title: Shell Scripting Basics - Beginner's Guide
slug: shell-scripting-basics
featured: true
draft: false
ogImage: /assets/blog/shell-scripting-basics.webp
tags:
  - shell
  - bash
description:
  Shell scripting is the code that is designed to run in the Unix shell.
  This means that you can write these generic pieces of instructions and execute
  them directly from the shell on Linux and MacOS.
conicalUrl: https://dev.to/abdadeel/shell-scripting-basics-beginners-guide-1h2b
---

![Shell scripting basics - Beginner's guide | abdadeel](@assets/blog/shell-scripting-basics.webp)

## Table of contents

## Introduction

## What is shell scripting? 😕

![confused_person](https://media.giphy.com/media/3o7btPCcdNniyf0ArS/giphy.gif)

Shell scripting is the code that is designed to run in the `Unix` shell. This means that you can write these generic pieces of instructions and execute them directly from the shell on `Linux` and `MacOS`. If you want similar functionality on your Windows machine, you can use the `shell/bash` alternative for windows like [Gitbash](https://git-scm.com/). In this article, together we will have a brief look at the syntax and basics of **shell scripting** and some of the examples to see some practices examples of shell scripting.

`.sh` is the extension for shell files. So if you want to follow along, you can create a file in your desired directory i-e `myscript.sh`, and open the file in your favorite text editor or IDE.

**NOTE: ⚡**
Before you start executing the bash files, you might need to give the file proper permissions to execute the shell script. For that, open the terminal and navigate to the same directory as your script file and execute the following command there.

```bash
chmod +x ./myscript.sh
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635001682266/WqLxBZspT.png)

## Log the `Hello World 🙂`

Let's start with the good old `hello world` example. To log anything to the console, use `echo` followed by whatever you want to log.

```bash
#! /bin/bash

echo "hello world 🙂"

```

adding `#! /bin/bash` represents the path to the bash.

## Comments

Comments in shell script start with `#` and are completely ignored when executing.

```bash
# This is a comment
echo "hello world"

# This is also a comment
```

## Variables

Variables in shell scripting are declared as below.

```bash
NAME="AB"

# log the name
echo $NAME
# or
echo ${NAME}

# Output:
# AB
```

Variables in shell scripting:

- should contain letters, numbers, and underscores
- are UPPERCASE by convention

## Reading User Input

Below is how you can take and input from the user and store the value in a variable `NAME`.

```bash
read -p "Enter your name: " NAME
echo $NAME

```

# Conditionals - `if` statement

The structure and syntax to define the `if` statements in the shell are given below. It starts with `if` followed by the condition in square brackets `[]` and action block and ends with the reverse of `if` which is `fi`.

```bash
read -p "Enter your name: " NAME

if [ "$NAME" == "AB" ]
then
    echo "Hello AB"
else
    echo "Hello World"
fi

# Output
# Enter your name: AB
# Hello AB

```

For else-if statements do,

```bash
read -p "Enter your name: " NAME
if [ "$NAME" == "AB" ]
then
    echo "Hello AB"
elif [ "$NAME" == "John"]
then
    echo "Hello John"
else
    echo "Hello World"
fi

# Output
# Enter your name: John
# Hello John

```

# Comparision Operators

Comparison operators are used for comparing two values i-e if they are equal, not equal, one is greater, greater or equal, etc.

In shell scripts, below is the syntax for how you can compare different values.

```bash

NUMBER_1=7
NUMBER_2=10

if [ "$NUMBER_1" -lt "$NUMBER_2" ]
then
    echo "$NUMBER_1 is less than $NUMBER_2"
elif [ "$NUMBER_1" -gt "$NUMBER_2" ]
then
    echo "$NUMBER_1 is greater than $NUMBER_2"
else
    echo "$NUMBER_1 is equal to $NUMBER_2"
fi

# Output
# 7 is less than 10
```

Below is the table of other available options

- `-eq` : `num1` -eq `num2` -> `True` if `num1` is equal to `num2`
- `-ne` : `num1` -ne `num2` -> `True` if `num1` is not equal to `num2`
- `-gt` : `num1` -gt `num2` -> `True` if `num1` is greater than `num2`
- `-ge` : `num1` -ge `num2` -> `True` if `num1` greater than or equal to `num2`
- `-lt` : `num1` -eq `num2` -> `True` if `num1` is less than `num2`
- `-le` : `num1` -eq `num2` -> `True` if `num1` is less than or equal to `num2`

# Logical Operators

Logical operators combine two conditions for the final result. The common logical operators are `AND` and `OR`. Let's see how we can implement them in a shell script.

The syntax for `AND` is `&&` and for `OR` is `||`. Here is an example of using them.

```bash
NUMBER_1=7
NUMBER_2=10
if [ "$NUMBER_1" -lt "$NUMBER_2" ] && [ "$NUMBER_1" -gt "0" ]
then
    echo "$NUMBER_1 is less than $NUMBER_2"
else
    echo "$NUMBER_1 is greater than $NUMBER_2"
fi

# Output:
# 7 is less than 10
```

# Case Statement

Case statements might be a little too much for a newbie to remember because of their weird syntax. After each condition there is an extra `)` and if none of the cases is true, its default to `*` block which behaves similar to `default` like in `Javascript`. Have a look at the example below for a deeper understanding.

```bash

read -p "Are you 18 or older: y/N: " ANSWER
case "$ANSWER" in
    [yY] | [yY][eE][sS])
        echo "You can drive!"
        ;;
    [nN] | [nN][oO])
        echo "You cannot drive"
        ;;
    *)
        echo "Invalid input"
        ;;
esac

: '
Output:

Are you 18 or older: y/N: yes
You can drive!

Are you 18 or older: y/N: y
You can drive!

Are you 18 or older: y/N: no
You cannot drive
'

```

# Simple `for` loops

Below is the simple syntax and structure of defining a for loop in a bash script.

```bash
for i in {1..5}
do
    echo "Number: $i"
done

: '
Output:

Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
'
```

Loop over a list of given names

```bash
# Declare an array
declare -a NAMES=("AB", "Kevin", "Lia", "John")
for NAME in "${NAMES[@]}"
    do
        echo "Hello $NAME"
done

: '
Output:

Hello AB,
Hello Kevin,
Hello Lia,
Hello John
'
```

# `while` loops

The syntax for `while` loops is similar to `for` loops.

```bash

COUNT=1
while [ "$COUNT" -le 5 ]
do
    echo "Number: $COUNT"
    ((COUNT++))
done

: '
Output:

Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
'
```

# `Functions`

Functions work the same as they do in programming languages except in shell, they don't directly accept any argument but use placeholders in the function body as you will see in the example below.

```bash
sayHello() {
    echo "Hello World"
}
sayHello

: '
Output:
Hello World
'
```

Function with arguments.

```bash
# function to add tow numbers
function add () {
    SUM=$(($1 + $2))
    return $SUM
}

# call the function
add 7 3
echo "Sum: $SUM"

: '
Output:
Sum: 10
'
```

# General Commands

All the UNIX commands can be executed through the shell script like creating folders and files, reading and writing files, etc.

Below are some resources where you can learn about the basic commands:

- [Learn basic commands for Linux, a free and open-source operating system that you can make changes to and redistribute.](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners)
- [Basic Linux Commands](https://hackr.io/blog/basic-linux-commands)

Below is the example of first creating a folder `myfolder`, creating a `.txt` file in that folder, and writing to that file.

```bash
#! /bin/bash

mkdir myfolder
touch "myfolder/myfile.txt"
echo "hello world" >> "myfolder/myfile.txt"

```

# Where can I use shell scripting

You can use shell scripting to run any sequence of commands either on the server or on your local machine. Below are some real-world examples of shell scripting.

Here is a shell script that is hypothetically running on a server inside a docker container and waiting for the database to be available before starting the server. As soon as the database is up and available for connection, the server starts.

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

Another great example would be automating the GitHub commits and pushes (basic).

```bash
#! /bin/bash

git add --all
git commit -m "$1"
git push origin master

```

here `$1` represent the extra flag/info you can pass to the script when executing the `.sh` file from the shell.
The execution will be:

```bash
./myfile.sh "your commit message here"
```

For more web dev content and resources, please join [my Twitter](https://twitter.com/abdadeel_) family by following [@abdadeel\_](https://twitter.com/abdadeel_).

Let's end it here and if you want to learn more advance shell scripting, please comment for part II. I would love to hear your ideas on what you want to implement through shell scripting and make your terminal life easier 😁.

Thanks
