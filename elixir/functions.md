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

## Recursion

Let's try and solve a simple problem with recursion: writing a function that given a base and an exponent, calculates the power.

```elixir
defmodule SimpleMath do
  def power(base, exponent) do
    power_helper(base, exponent, 1)
  end

  defp power_helper(_base, 0, product_so_far) do
    product_so_far
  end

  defp power_helper(base, exponent, product_so_far) do
    power_helper(base, exponent - 1, (base * product_so_far))
  end
end
```

Some things to note:
- The function `power` calls a helper function.
- There is a standard helper function calling itself.
- The base case happens when Elixir matches the exponent to 0.
- The `_` tells Elixir that the `base` parameter will not be used in the defined function. It still needs to appear for the matching.

We can also use 'guards', meaning executing a function only when certain conditions are met. This is done via the `when` keyword:

```elixir
def power(_base, exponent) when exponent == 0 do
  1
end
```

Let's add a prime checking function to see a different example:

```elixir
def is_prime?(potential_prime) when potential_prime <= 1 do
  false
end

def is_prime?(potential_prime) do
  prime_check(potential_prime, 2)
end

defp prime_check(potential_prime, current_val) when current_val === potential_prime do
  true
end

defp prime_check(potential_prime, current_val) when rem(potential_prime, current_val) === 0 do
  false
end

defp prime_check(potential_prime, current_val) do
  prime_check(potential_prime, current_val + 1)
end
```
