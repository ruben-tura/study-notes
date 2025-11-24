---
title: Enum and ranges
parent: Elixir
nav_order: 4
---

# Enum and ranges

A range can be defined using the simple syntax `1..10`.

Ranges are not useful by themselves, but we can combine them with the `Enum` module:
```elixir
Enum.each(1..10, &IO.puts/1)
```

The `&` is used to make a reference to an existing function. We can also use anonymous functions!

```elixir 
Enum.each(1..10, fn (val) -> IO.puts(val) end)
```

The following are two ways to write the same thing:

```elixir 
Enum.each(1..10, fn (val) ->
  root = SimpleMath.sqrt(val)
  IO.puts(root)
end)

Enum.each(1..10, &(IO.puts(SimpleMath.sqrt(&1))))
```

The `map` function executes code on each element, and returns a new collection of values:

```elixir 
squares = Enum.map(1..10, fn (val) -> SimpleMath.power(val, 2) end)
Enum.each(squares, &IO.puts/1)
```

A way to use the pipe operator to concatenate some `map` functions:

```elixir 
Enum.map(1..10, fn (val) -> SimpleMath.power(val, 3) end)
|> Enum.map(fn (cube) -> SimpleMath.sqrt(cube) end)
|> Enum.each(&IO.puts/1)
```

`filter` returns a collection with only the elements passing the test:

```elixir 
primes = Enum.filter(1..100, fn (val) -> SimpleMath.is_prime?(val) end)
Enum.each(primes, &IO.puts/1)
```

`reject` does the opposite:

```elixir 
non_primes = Enum.reject(1..100, fn (val) -> SimpleMath.is_prime?(val) end)
Enum.each(non_primes, &IO.puts/1)
```

`reduce` reduces items in a collection to a single value:

```elixir 
primes = Enum.filter(1..10, fn (val) -> SimpleMath.is_prime?(val) end)
sum = Enum.reduce(primes, 0, fn (prime, sum_of_primes) -> prime + sum_of_primes end)
IO.puts("The sum of the primes is #{sum}")
```

`any?` and `all?` return true if any or all of the elements pass the test:

```elixir 
any_prime = Enum.any?(1..10, fn val -> SimpleMath.is_prime?(val) end)
IO.puts("It is #{any_prime} that there is at least one prime in that range")

all_prime = Enum.all?(1..10, fn val -> SimpleMath.is_prime?(val) end)
IO.puts("It is #{all_prime} that all the values in that range are prime")
```
