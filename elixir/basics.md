---
title: Basics
parent: Elixir
nav_order: 1
---

# Basic Data Types

## Integers

Elixir supports standard integers, and also binary, octal and hexadecimal with the `0b`, `0o` and `0x` prefixes.

## Floats

Floating points numbers require a decimal after at least one digit. They support `e`.

## Booleans

Boolean values are either `true` or `false`. Everything is truthy aside from `false` and `nil`.

## Atoms

An atom is a constant whose name is its value. They are defined like `:foo`.

The boolean values also corresponds to the atoms `:true` and `:false`.

```elixir
iex> is_atom(true)
true
iex> is_boolean(:true)
true
iex> :true === true
true
```

In Elixir, names of modules are also atoms. Atoms are also used to reference modules from Erlang libraries, including built in ones.

## Strings

In Elixir, strings are UTF-8 encoded and wrapped in double quotes.

# Basic Operations

## Arithmetic

The standard `+`, `-`, `*` and `/` operators work as expected. `/` always returns a float.
To make an integer division, you can use either `div(10, 3)` or `rem(10, 3)` for the remainder.

## Boolean

Again, standard `||`, `&&` and `!` operators work as expected. In Elixir, only `false` and `nil` are falsy values, and everything else is truthy, including empty strings or lists.
You can also use `or`, `and` and `not`, but the first argument must always be a boolean.

## Comparison

Again, same operators as always, with `==`, `!=`, `===` (for strict comparison), `!==`, `<=`, `>=`, `<` and `>`.

Any two types can be compared, and it is useful in sorting. The sorting order is: `number < atom < reference < function < port < pid < tuple < map < list < bitstring`.

## String Interpolation

```elixir
iex> name = "Sean"
"Sean"
iex> "Hello #{name}"
"Hello Sean"
```

## String Concatenation

String concatenation uses the `<>` operator:

```elixir
iex> "Hello " <> name
"Hello Sean"
```

## Match

In Elixir, the `=` operator indicates a match, and not an assignment. This means that in a code like `age = 50`, Elixir is looking to make it true, and it does so by binding the name `age` to the value `50`. Rebinding is possible.

A statement like `50 = age` would still be ok for Elixir, as all it does is look for a match. A statement like `5 = age` would still theoretically be ok, but Elixir looks at the value of `age`, and being that 50 and 5 are not equal, it returns a Match Error. 

For Elixir to be able to make a binding, the name to bind must be in the left hand side of the match operator `=`.