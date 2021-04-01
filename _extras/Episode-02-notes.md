# Notes for julia-novice episode 2

## Calculating with numbers

Once you have started the REPL or a Jupyter notebook, you can use it as a calculator by typing in calculations and pressing `enter` (REPL) or `ctrl` + `enter` or `shift`+`enter` (Jupyter)

```julia-repl=
1 + 2
```
You can do many calculations on the same line
```julia-repl=
1 + 2 * 3
```
use parenthesis to change the order
```julia-repl=
(1 + 2) * 3
```
do divisions, squares, etc
```julia-repl=
2 / 13
3 ^ 3
```
To use large floating point numbers, use scientific notation
```julia-repl=
1e2 / 3
```
Note that by default julia does not convert the type of the number, eg. the result of calculating with integers is an integer. This can lead to overflow, so check your results if in doubt.
```julia-repl=
64 ^ 20
64.0 ^ 20
```
Some operations, such as `/` convert the type
```
4 / 3
```
For integer division, use `\div` 
```
4 \div 3
```

## Using Variables

You can assign a value (of any type) to a variable
```julia-repl=
age = 25
name = "Bob"
```
and access the value by the name of the variable
```julia-repl=
age
```
Normally the result of the last assignment is printed out. Add `;` at the end of the line to suppress the output
```julia-repl=
age = 25;
```
You can print the values of variable(s) to the screen with `prinln`
```julia-repl=
println(name,bob)
```
How to improve the formatting? You can concatenate strings with `*`
```julia-repl=
name * " likes " * "burritos"
```
We can use this to print
```julia-repl=
println(name * " is ", age)
```
Note that `println(name * " is " * age)` gives an error. The type of `age` is a number and for numbers `*` means something else!

## Calculating with variables

We can substitute variables into the basic math operations from before
```julia-repl=
age + 3
```
Note that this just prints the result of the calculation, it does not change `age`. We can access the result using the special variable `ans`
```julia-repl=
println(ans)
```
We can also assign the result into another variable
```julia-repl=
age_in_months = age * 12
```
We can also substitute variables into print statements (or any other kind of statements)
```julia-repl=
println("In 10 years " * name * " will be ", age + 10)
```
What happens if we update `age` and try the same statement again?
```julia-repl=
age = age + 3
println("In 10 years " * name * " will be ", age + 10)
```
### Useful shorthands

You can omit `*` between a number and a variable. This makes equations look cleaner.

```julia-repl=
x = 3
3x - 2x^2
```

To increment the value of a variable, you don't need to type it's name twice

```julia-repl=
x = 3
x += 5
x /= 2
println(x)
```

## Excercises on variables

From python lesson?

## REPL modes

In REPL you will see the prompt change to remind you which mode you are in. In Jupyter you have to type the special character every time.

Exit the mode with `Backspace`

### Help mode `?`

To get more information about a function or operator.

```julia-repl=
?*
```

### Package mode `]`

This is where you carry out package management tasks such as adding packages, testing them, and so on. You can see the status of your installed packages with

```julia-repl=
]status
```

You should see the `IJulia` package we added at the beginning!

### Shell mode `;`

If you want to use the commands from the shell lesson, you can do so in shell mode

```julia-repl=
;ls -aFlh
```

## Unicode characters

You may come across some non-arabic characters in Julia and are allowed to use them. To find them, precede your command with `\` and press `tab` to autocomplete. For example

```julia-repl=
\Lambda = 4
\alpha = 5
2\alpha + \sqrt\Lambda
```

Julia uses some internally, for example

```julia-repl=
pi
```

Emojis start and end in `:`, use them at your own risk

## Arrays

We often need containers that hold multiple values in one variable. In Julia you most often use *tuples* or *arrays*. Arrays are usually good for data of a single type. You can define an array using `[]`
```julia-repl=
[1,2,3]
```
and assign this to a variable as before
```julia-repl=
my_array = [1,2,3]
```
You can access elements of the array by slicing using `[]` *Note that indexing starts at 1 by default*.
```julia-repl=
my_array[2]
```
Array slices can be used like variables
```julia-repl=
println(my_array[2] - my_array[3])
```
We can multiply an array with a scalar by
```julia-repl=
my_array * 3
```
But if we try to add a scalar to an array we get an error because the method is not defined
```julia-repl=
my_array + 2
```
The error message gives a hint `For element-wise subtraction, use broadcasting with dot syntax: array .- scalar`. Broadcasting is very powerful, more on that later. For now we can perform the operation element-wise by using
```julia-repl=
my_array .+ 2
```
Arrays can have multiple dimensions
```julia-repl=
my_2d_array = [1 2 3; 4 5 6]
```
We can slice by dimension, and use *ranges*
```julia-repl=
my_2d_array[1:2,3]
```
Arrays of higher dimensions are better to create using the constructor `Array`
```julia-repl=
my_4d_array = Array{Float64,4}(undef, 4, 5, 2, 3)
```
or using functions such as `fill` or `zeros`
```julia-repl=
?fill
?zeros
```
```julia-repl=
fill(pi/2, (3,3))
```