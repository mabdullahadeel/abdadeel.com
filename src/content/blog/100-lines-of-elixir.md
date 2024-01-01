---
author: Abdullah Adeel
pubDatetime: 2021-12-08T15:22:00Z
modDatetime: 2024-01-01T19:20:05Z
title: 100 lines of Elixir
slug: 100-lines-of-elixir
featured: true
draft: false
ogImage: /assets/blog/100-lines-of-elixir.webp
tags:
  - elixir
description:
  Elixir is a multi-purpose dynamically typed functional programming language which
  when combined with the phoenix web framework is one of the hottest topics out there.
conicalUrl: https://dev.to/abdadeel/100-lines-of-elixir-2img
---

![100 lines of elixir | abdadeel](@assets/blog/100-lines-of-elixir.webp)

## Table of contents

## Introduction

Elixir is a multi-purpose dynamically typed functional programming language which when combined with the phoenix web framework is one of the hottest topics out there. Even though elixir is a pretty new player in the market launched in 2011, the roots are pretty deep since it runs on [Erlang VM](https://www.erlang.org/). This means that it highly infers the characters of Erlang VM and provides a much simpler, easy to read and maintainable codebase. Erlang being built by a telecommunication company named [Erricson](https://www.ericsson.com/en) back in the '80s, highly focuses on concurrent connections and [fault tolerance](https://en.wikipedia.org/wiki/Fault_tolerance)
To learn more about Erlang, click [here](https://serokell.io/blog/history-of-erlang-and-elixir)

![yahoo](https://media.giphy.com/media/TdfyKrN7HGTIY/giphy.gif)

In other words, if `concurrency`, `scalability`, and `reliability` are the main concerns of your application, Elixir is one of the best choices out there. That's it for theoretical introduction, and time to get hands dirty with some elixir code.
To start, you'll first have to install both Erlang and Elixir on your machine. To install on your respective operating system, visit [installation guide](https://elixir-lang.org/install.html).
After you have successfully installed Elixir, you should be able to type the following command in your terminal without any error.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638900996243/hFj-Mu27g.png)

After this, type `iex` in your terminal and this should start an interactive elixir shell and you should be able to perform basic arithmetic operators there as shown below.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638901176734/MSen0Zdzh.png)

This interactive shell is good for basic things but if you want to work with a large elixir codebase, it's obvious that you need an IDE or text editor. Obviously 😁.
For that, use `mix` to create a new elixir project. `mix` is the dependency and command line manager for elixir. Think of it as `npm` for node, `cargo/rustc` for rust, or `pip` for python.
`cd` to your desire directory where you want to create a new elixir project and run the following command.

```elixir
mix new my_project
```

and then open the folder in your favorite text editor.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638901856439/EbbQKhyDV.png)

Looking at the folder structure, you can see that `mix` pretty much set up the whole project for you including the `git` initializing. The main application code lives in the `lib` folder. Another cool thing about the elixir is that it comes pre-configured with very good testing support. `mix.exs` is the file, where mix keeps track of all the project dependencies just like a `package.json` file for `node`. Now it's time to see some elixir magic. Open `lib/my_project.ex`. Remember, the name of the file in the `lib` folder would be the same as the name of your project. When you open the file, the default module is something like this 👇.

```elixir
defmodule MyProject do
  @moduledoc """
  Documentation for `MyProject`.
  """

  @doc """
  Hello world.

  ## Examples

      iex> MyProject.hello()
      :world

  """
  def hello do
    :world
  end
end

```

Even though the elixir is a functional programming language, but it provides a lot of macros that help you organize the code into manageable modules to abstract away all the logic into one module and you don't need to even export these modules to use them in other modules.
In the above snippet, you see a lot of words starting from `@` are the attributes. Elixir has a built-in docs generator and you can use tools like `ex_doc` to generate the docs from the `@moduledoc` and `@doc` attributes. To start, add the following dependency to `deps` function in `mix.exs` so that it looks something like this 👇.

```elixir
  def deps do
    [{:ex_doc, "~> 0.21", only: :dev, runtime: false}]
  end
```

Then run the following command to install the dependency in your project.

```elixir
mix deps.get
```

To generate docs, run the following command and it should create a new folder name `doc` in project directory with all the HTML files for the documentation.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638903772564/EIGwGxhFd.png)

Execute the following command to generate docs

```elixir
mix docs
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638903865179/5nH6Wndzg.png)

Opening `index.html` with `liveserver` will reveal docs.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638904004002/DyAwjvhsa.png)

<hr>

Enough for the docs, let's run some code.

Add a function named `hello` under the `MyProject` module. This function simply prints the `"world"` string to the terminal. To call this function, go the terminal in the current project directory and execute the following command.

```elixir
iex -S mix
```

This will open an `iex` session but this time, it will compile all the application code and import the modules into the current `iex` session.
To execute the function that you wrote, run the following 👇.

```elixir
iex(2)> MyProject.hello
world
:ok
iex(3)>
```

This was a brief introduction to the Elixir. In the future, I'll be releasing a series on the basics of elixir so that it's easier for beginners to understand this phenomenal functional language and build the next big Discord.

### Fun fact

Discord is one of the early adopters of `Elixir` and today, elixir is paying back by handling billions of messages and calls per day on the platform.

For more web-development content, please follow me on [twitter](https://twitter.com/abdadeel_) [@abdadeel\_](https://twitter.com/abdadeel_) . See you there !
