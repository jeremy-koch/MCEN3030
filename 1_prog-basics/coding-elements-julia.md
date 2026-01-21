# Necessary Coding Elements -- Julia

If you are interested in computational science, you might find Julia to be an interesting language. Maybe you'd like to read this: [Julia: A Fresh Approach to Numerical Computing](https://arxiv.org/abs/1411.1607).

The considerations outlined in that paper are not important to MCEN 3030, but, if you have the appetite for it, you could spend MCEN 3030 building up some relevant experience in some basic tasks, and then can expand to more cutting-edge things on the side or after the course has concluded.

There are a lot of extra considerations with Julia that will make it challenging for those who are unfamiliar with the vocabulary of computer science -- you will need to be more careful with data types and variable scope, as examples. For this reason, I think I'd like to chat with you before you commit to this language. Everyone in the class could use it and would be fine, but I just want to make sure the juice is worth the squeeze (for your situation). That being said, I would be really interested to get some more experience myself with a handful of brave students.

Julia is famous for "multiple dispatch" which is something we will not really have an opportunity to explore in this class. However, you may independently explore this, and tell me about it!

## Functions

Here is a file with a couple functions in it, and a couple function calls:
```julia 
function my_first_fxn(a, b)
    c = a + b
    return c
end

function my_second_fxn(a, b)
    c = a - b
    d = 2 * a
    return c, d 
end

C_1 = my_first_fxn(3, 2)
C_2, D_2 = my_second_fxn(3, 2)
```

The Rules:
- Functions begin with a line that includes ```function```, a function name, and the input variables(/arguments).
- The output of the function is whatever follows the ```return```. Could be one number or one array or multiple numbers or multiple arrays. An ```end``` must be included as well -- it's a bit clumsy.
- There is something called "implicit return", where the last thing that is evaluated is the thing that is returned. Probably being explicit (as we are above) is the more careful thing to do.
- If there are multiple outputs, you must "prepare" your script for them, as I did above with the ```C_2,D_2=```.


## Creating vectors/matrices/arrays


```julia
x1 = 0:0.1:2                      # start:step:stop (creates a range object)
x2 = range(0, 10, length=500)     # 500 points between 0 and 10
x3 = 10 .^range(4, 7, length=500) # 500 log-spaced points between 10^4 and 10^7
A = [1 2 3; 4 5 6]                # a matrix is built with spaces separating columns and semicolons separating rows

y = zeros(1, length(x2))    # a row vector full of zeros with the same length as x2
z = ones(1, length(x2))     # same, but full of ones
A = zeros(4, 4)             # a 4x4 matrix of zeros

using LinearAlgebra         # Required for eye (I) and diag functions
B = Matrix(1.0I, 4, 4)      # diagonal is full of ones, rest zero
D = diagm(0 => [5, 3, 1])   # diagonal is 5,3,1, rest zero
D2 = diagm(1 => [5, 3, 1])  # the first diagonal above the main is [5,3,1]... so this is a 4x4 matrix

r = rand(1, 5)              # 1x5 row matrix of random numbers
R = rand(4, 4)              # same, but a 4x4 matrix
```


## Indexing and Modifying Elements

Julia indexes from ```1``` and can use ```end``` to refer to the last index. Be careful when talking to Python folks, your "first" element might be their "zeroth". (MATLAB indexes from 1.)

Julia is consistent with the following rule: if it applies to multiple elements, the operation is "dot something". Both MATLAB and Julia have the ```.^``` and ```.*``` for element-by-element math, but Julia has the peculiar ```.=``` when setting multiple values of an array. It makes sense, if you think about it, but also I am not sure if ```x[3:end]=0``` (which is how MATLAB would do it) is actually that ambiguous!

```julia
x[i] = 5                    # changes the ith element of x (x would need to exist already)
x[3:end] .= 0               # elements 3 to the end become 0
x[2:4] .= -88               # elements 2, 3, and 4 becomes -88

A[4, 1] = 5                 # changes the fourth element in column 1
A[:, 5] .= 6                # the fifth column is a vector... this makes all of those elements equal 6
A[4, :] .= -9               # the fourth row is now full of -9s
```




## Doing math with them

```julia
x=[1, 2, 3]         # with commas... this creates a column vector
y=[4, 5, 6]
# the same without commas would create a row vector
z=x.*y
```
From the above code, we would find ```z=[4, 10, 18]```. To square all elements, ```.^2```, to divide element-by-element, ```x./y```. No dot is needed for addition and subtraction.

The "dot something" structure applies to basic mathematical functions too, which is kind of annoying: ```sin.(x)```, ```exp.(x)```, ```log.(x)``` is the natural log, ```log10.(x)``` is the base-10 log, ```sqrt.(x)``` for square root. sin, cos, tan, etc., are a similar pattern.


## Conditional Statements
Here is the ```if```-```elseif```-```else``` structure:

```julia
if x<5
    y=10
elseif x>9
    y=15
else
    y=-99
end
```

The "logical equals" is ```==``` (as in, ```x==5``` checks to see if ```x``` is equal to ```5```, evaluating that as True/False or 1/0). The logical and is ```&&```, the logical or is ```||```, and ```>=``` and ```<=``` work as you'd expect! "Not equals" is ```!=```. 

Julia has something called "the ternary operator", which is a succinct way to write a "condition, value if true, value if false" statement: ```y = x < 5 ? 10 : -99```.

## Loops
A ```while``` loop looks like this:
```julia
counter = 0
while counter < 5
    println("hi")
    counter += 1
end
```
...but ```for``` loops (and maybe ```while``` too, in another application?) have a "gotcha": variables within a ```for``` loop have scope limited to within the loop, by default (and maybe only within scripts or the REPL?). Declaring the variables ```global``` is necessary to adjust them overall. So:
```julia
x = [1, 2, 3]
S = 0
for i in 1:length(x)
    global S = S + x[i]
end
```
... has that ```global``` declaration, which is not needed in MATLAB/Python. However, wrapping the summation in a function eliminates the need:
```julia
function sum_em(z)
    S=0
    for z_i in z
        S += z_i  # No 'global'
    end
    return S
end

x = [1, 2, 3]
S=sum_em(x)
```
We will end up using ```for``` loops a lot in this class, and so this will be something to keep an eye out for. 

## Reading/Writing Spreadsheets

It is common to use ```*.csv``` files: comma-separated values. You may be able to load from other sources, but csv will be our standard because of the predictability of the formatting.

In Julia, some additional packages are necessary: CSV.jl and DataFrames.jl. (I haven't tried this yet but apparently both are needed?) And then the beginning of your script will be
```julia
using CSV
using DataFrames

# This reads the file into a "DataFrame" (similar to a MATLAB Table)
df = CSV.read("my_data.csv", DataFrame)

# Convert the DataFrame to a plain Matrix
data = Matrix(df)

# OR: Read it directly as a matrix without headers
data = CSV.read("my_data.csv", Tables.matrix)
```

To write a csv:
```julia
using CSV

x_data = [1, 2, 3]
y_data = [10, 20, 30]

# [x_data y_data] creates a matrix with two columns
data_matrix = [x_data y_data]

# Write to file (header is optional)
CSV.write("data.csv", Tables.table(data_matrix), header=["X", "Y"])
```

There is also a built-in option that, for whatever reason, is discouraged: ```using DelimitedFiles``` then ```data = readdlm("my_data.csv", ',')``` would load-in data, and ```writedlm("data.csv", data_matrix, ',')``` would write a new csv.

## Anonymous Functions

In our root-finding algorithms, we will input a (mathematical) function into a (programming) function, e.g.: find the root of $f(x)=\sin(x)-0.85$. This can be achieved via an anonymous function: ```f = x -> sin(x) - 0.85``` or ```f(x) = sin(x) - 0.85```. And remember: to use a function with an array we use the "dot something" structure: ```f.([1,2,3])```.

If two inputs are needed: ```f = (x, y) -> x + y``` or ```f(x,y) = x+y```.




# break, continue, and return

When you are within a loop, ```break``` immediately breaks you out of the loop entirely. So, for example:
```julia
S=0
for i in 1:500
    if i==5
        break
    end
    global S+=1
end
println(S)
```
You should see that ```S``` is 4.

When you are within a loop, ```continue``` immediately sends you back to the top of the loop. So, for example:
```julia
S=0
for i in 1:5
    if i==2 || i==3
        continue
    end
    global S+=1
end
println(S)
```
You should see that ```S``` is 3.

You can ```return``` from anywhere in a function. So, for example:
```julia
function my_fxn(x)
    if x==0
        return 0
    end
    return 15
end

println(my_fxn(0))
println(my_fxn(1))
```
You should see that the first print produces 0, the second produces 15.








## Some common motifs

If you need something to happen if a number is even:

```julia
if x % 2 == 0  # Even!
    # do something
else           # Odd!
    # do something else
end
```
... but actually Julia has built-in commands: ```iseven(x)``` and ```isodd(x)```.





## A few frustrations

A few frustrations I have encountered (and most of these are likely just because I am more used to MATLAB/Python, which are more novice-friendly):
- ```y = x``` will assign ```y``` to the same memory location as ```x```, which means that changing ```x[1]``` also changes ```y[1]```. If you need to make a genuine copy that can be independently modified: ```y=copy(x)```.
- Meanwhile, slicing an array makes a copy automatically. ```z=x[2:end]``` creates an independent array, ```z``` that is not tied to ```x```.
- Keep an eye on the variable scope within ```for``` loops.
- The compile times within VS Code (on the few functions I have written... I am learning too!) have been borderline unnoticeable, just a 2-3 second hiccup the first time you run after major changes. Second time, fast. For MCEN 3030, with our smaller functions, this may be a bit of a frustration... until we get to the machine learning project, where I am hopeful compiling will knock the training time down considerably. It is not awful in Python... I am doing a project where it might take 40 seconds to train the model, but I wonder if I switched over to Flux, would be like 5 seconds? I'll be interested to see!





## Additional resources/readings

https://github.com/brenhinkeller/JuliaAdviceForMatlabProgrammers
