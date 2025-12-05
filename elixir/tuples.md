---
title: Tuples
parent: Elixir
nav_order: 5
---

# Tuples

Tuples are array-like data structures, but data in Elixir is immutable.
We can technically update or add elements in a tuple, but it is not as simple as storing a new element in an array; the old state of the array must always be available.
Hence, tuples tend to be used for collections of unchanging data, like a group of values returned from a function.
They can also be used in pattern matching.
Values in a tuple don't have to be of the same type.
```elixir
full_name = {"Mark", "Robert", "Mahoney"}
IO.puts("There are #{tuple_size(full_name)} elements in the tuple")

first = elem(full_name, 0)
middle = elem(full_name, 1)
last = elem(full_name, 2)
```

Tuples can be used in pattern matching, and in the following instruction the values inside the curly braces are names that Elixir will try to bind to values:
```elixir
{first, middle, last} = full_name #{"Mark", "Robert", "Mahoney"}
```
Remember that you can use an underscore `_` to tell Elixir you don't care about that positional value.

We can also use `put_elem` to create a new binding. This will not modify the original tuple, as it is immutable, but will refer to it for all values which need to be the same. For example, let's see how to create two tuples, one containing the first and last name of the 26th president of the USA Teddy Roosevelt and the other containing the same data about the 32nd president: Franklin Roosevelt.

```elixir 
pres_num_26 = {"Teddy", "Roosevelt"}
pres_num_32 = put_elem(pres_num_26, 0, "Franklin")
IO.inspect(pres_num_32)
IO.inspect(pres_num_26)
```

Let's see an example of pattern matching using tuples and atoms:
```elixir 
defmodule NameFormatter do
  def format({:full_name, first, middle, last}) do
    "#{last}, #{first} #{String.first(middle)}."
  end

  def format({:partial_name, first, last}) do
    "#{last}, #{first}"
  end

  def format({:solo_name, first}) do
    "The one and only #{first}"
  end
end

name = NameFormatter.format({:full_name, "Mark", "Robert", "Mahoney"})
IO.puts(name)
name = NameFormatter.format({:partial_name, "Jack", "Kerouak"})
IO.puts(name)
name = NameFormatter.format({:solo_name, "Cher"})
IO.puts(name)
```

Elixir checks the first value of the tuple for an atom, and when it finds it, it calls the corresponding function by binding as specified.

Supposing we have a file named `name.txt`, let's see what happens when we try and read it:

```elixir 
result = File.read("name.txt")
IO.inspect(result) #this prints {:ok, "Mark Robert Mahoney"}
```
We could use pattern matching to separate the returned data:
```elixir 
{status, contents} = File.read("name.txt")
```

Let's see how to deal with potential errors:
```elixir 
defmodule FileHelper do
  def read_file_and_print(file_path) do
    handle_read_results(File.read(file_path))
  end

  def handle_read_results({:ok, file_contents}) do
    IO.puts(file_contents)
  end
  
  def handle_read_results({:error, :enoent}) do #error no entry
    IO.puts("The file does not exist")
  end

  def handle_read_results({:error, :eisdir}) do #error is a directory
    IO.puts("You specified a directory not a file")
  end
end
```
Again, you could pattern match a generic error type using `def handle_read_results({:error, _})`

