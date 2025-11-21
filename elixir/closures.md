
---
title: Closures
parent: Elixir
nav_order: 3
---

# Closures

We can bind to a name an anonymous function like so:
```elixir
retirement_fn = fn (retirement_age, current_age) ->
  retirement_age - current_age
end
```
Anonymous functions are just data. We call it like so:
```elixir 
years_until_retirement = retirement_fn.(67, 49)
IO.puts("You have #{years_until_retirement} years until retirement")
```
In the following code we return an anonymous function as the last statement of the `get_retirement_fn` function.
```elixir
defmodule RetirementCalculator do
  def get_retirement_fn(retirement_age) do
    fn (current_age) ->
      retirement_age - current_age
    end
  end
end

optimistic_fn = RetirementCalculator.get_retirement_fn(60)
pesimistic_fn = RetirementCalculator.get_retirement_fn(100)
current_fn = RetirementCalculator.get_retirement_fn(67)

years_until_retirement = optimistic_fn.(49)
IO.puts("Optimistically, you have #{years_until_retirement} years until retirement")
years_until_retirement = pesimistic_fn.(49)
IO.puts("Pessimistically, you have #{years_until_retirement} years until retirement")
years_until_retirement = current_fn.(49)
IO.puts("You have #{years_until_retirement} years until retirement")
```
