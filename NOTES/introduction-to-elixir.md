erlang is a development that was build primarly for scalable and reliable systems, it was created in the mid 80's by a company called ericson which is a swedish telecom company and erlang was created based on the necessity of knowing the different phone calls in their switch boards in a way that the switch boards would be highly reliable, responsive, and scaleable 24/7.

If you look at software in the early 90's most software was limited to Desktop based and the need for high availibity was limited to specialised systems such as these telecom switch boards.
Today things have changed we have the internet & the web. Most applications are driven and supported by some kind of system that processes requests and crunches data then pushes the relevant information to many clients. So this pattern that was created inside of erlang, is extremely useful for web technology as well as imbedded technology.

This is where Elixir comes in, with Erlang you have a syntax that is very similar to something like Pearlog and this makes it very unapproachable to the average programmer because the syntax is a bit foreign and gross. Will Elixir on the other hand the sytax was written so that it would look more clean and it looks more like something like ruby.

You have the BEAM which stands for the people who invented this machine.
You have the BEAM which runs on one operating system thread, which has a bunch of Schedulers inside of it and these Schedulers manage the Processes. When talking about Processes we aren't talking about Operating System Processes instead we are talking about a concurrency primitive which is called a Process, an Erlang or an Elixir program can have literally million processes running all concurrently all inside of the application, these Schedulers can take these open cpu cores and then they spread the actual execution of the program across these cpu cores in a very even and nice distributed manner. By default when you write Elixir code everything is very opinionated and directed towards this distributed highly concurrent way of writting code.

Elixir & Erlang have a very similar compilation path, Elixir goes through and it is converted to `Elixir -> Erlang Abstract format -> Core Erlang -> BEAM VM bytecode`.

More specificly we have

`Elixir Source Code -> Initial Parsing -AST-> Macro Expansion -Expanded AST-> Bytecode generation`

AST is a big old tree with a bunch of information inside of it.

Something to keep in mind when proceeding with Elixir is that:

Every operation, every function, every block inside Elixir is considered to be an expression and the main idea behind expressions is that they always have a return statement.
So everything you write in Elixir code with always return something.

Because Elixir is a dynamic programming language we don't need to explicitly declare the types for a variable and we don't need to explicitly declare that we are creating a variable, the type of the variable is going to be determined by the data that is contained inside of it at that moment.

ie:

`x = 10`

x is now variable of type integer because it references the type of value of 10.
This is what is called variable binding inside of Elixir, the variable is actually used for pattern matching inside of Elixir.
Now you can think of it like you are binding the value of 10 to the variable of x.

`x / 2`

You can use operations on the variable as you would the actual value.
Now Elixir uses the Erlang type system, the type system itself is pretty simple and there are a lot of easy to understand primitives.

- integers
  `3` you can write them as an integer
  `0xFF` you can write them as a hex and it will be converted into a readable format
- floats
  `3.14159`
  `3.0e-2`
  `1 + 2`
  `3 * 4`
  `3 - 5`
  `5 / 2`
  `div 5, 2`
  `div(5, 2)`
  `rem(5, 2)`
  `1_000_000`

You can use extremely large numbers in Elixir.
If you are worried about memory size, the memory is done automatically, an integer will take up as much space as is needed. A float will either have a float that is 32 bit in size or 64 bit in size depending on the build architecture of the virtual machine.

- :atoms

Atoms are literal named constants, similar to symbols in Ruby.
Or enumerations in C or C++

`:atoms`
`:"an atom"`
`:"12387 &*^#2`

Now that atom itself consists of 2 pieces, there is the actual text then there is the value. The text is what ever you put after the `:` character and at runtime this text is kept inside of a structure called the atom table. The value is the data that goes into the variable, its merly a reference to the atom table. This is why atoms are used for named constants because the are both efficent in memory and in preformance.

You can bind a variable to an atom

`var = :atom`

The variable var doesn't contain the entire text of the atom but only a reference to the atom table. Therefor the memory consumption of this variable is fairly low and of course the code is still readable.

Another way to write an atom is to use an uppercase character

`AModule`

This is called an alias `AModule`

`AModule` is the same as `:"Elixir.AModule"`

When you use an alias, Elixir will implicatly add the Exlixir . prefix to its text then it will insert an Atom there.

`AModule == Elixir.AModule`
`true`

Aliases are useful because you can use them to rename existing Module names

```elixir
alias IO, as: MyIO
MyIO.puts "Hello"
Hello
:ok
```

elixir has boolean values

```elixir
> true
true
true
> false
false
false
```

Both of these values are actually atoms

```elixir
> :true == true
:true == true
true
```

```elixir
> :false == false
:false == false
true
```

```elixir
> true and false
true and false
false
> true or false
true or false
true
> not true
not true
false
```

Along with booleans we also have a special atom called nil, nil is like null in other programing langs

```elixir
> nil
nil
nil
> :nil
:nil
nil
```

Along with other languages the atoms `nil` & `false` are treated as falsy values where as everything else is treated as a truethy value

```elixir
> if 10 do
if 10 do
> IO.puts = "true"
IO.puts "true"
> end
end
true
:ok
```

```elixir
> if nil do
if nil do
> IO.puts "True"
IO.puts "True"
> end
end
nil
```

```
> IO.puts "True"
IO.puts "True"
> end
end
nil
> nil || false || 4 || true
nil || false || 4 || true
4
> true && 5
true && 5
5
> !5
!5
false
```
