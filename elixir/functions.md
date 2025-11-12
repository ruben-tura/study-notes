---
title: Functions
parent: Elixir
nav_order: 2
---

# Functions

## Modules

In Elixir, functions reside in modules, defined using the `defmodule` keyword:
```elixir
defmodule NameFormatter do
  
end
```
Note the name of the module starting with an uppercase letter.

## Functions

Functions are defined with the `def` keyword:
```elixir
defmodule NameFormatter do
  def format(first, middle, last) do
    "#{last}, #{first} #{String.first(middle)}."
  end
end
```

No return statement exists; all functions return the result of the last statement inside of them.

You can then call the function like so:
```elixir
formatted_name = NameFormatter.format("Mark", "Robert", "Mahoney")
IO.puts(formatted_name)
```

We could add another function which handles people with no middle name. We can give it the same name, as functions in Elixir are defined by their name and their arity, meaning in this case we would have a function called `format/2` and another one called `format/3`:
```elixir
defmodule NameFormatter do
  def format(first, middle, last) do
    "#{last}, #{first} #{String.first(middle)}."
  end

  def format(first, last) do
    "#{last}, #{first}"
  end
end
```

## Matching

We can also match a parameter in a function, so that a specific function will get called when a match occurs, for example:
```elixir
defmodule NameFormatter do
  def format("John", middle, last) do
    "#{last}, John (Jack) #{String.first(middle)}."
  end

  def format(first, middle, last) do
    "#{last}, #{first} #{String.first(middle)}."
  end

  def format(first, last) do
    "#{last}, #{first}"
  end

  def format(sole_name) do
    "The one and only #{sole_name}"
  end
end
```
In this case, if we pass "John" as first name, the first function will be executed.
Matching is checked from top to bottom, or rather, from the first declaration to the last. The first matching is the one that will be executed.
