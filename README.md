# Swirl
## 1. Basic Building Blocks 
R can be used as an interactive calculator. Type 5 + 7 and press Enter.
```
5 + 7
```
R simply prints the result of 12 by default. However, R is a programming language and often the reason we use a programming language as opposed to a calculator is to automate some process or avoid unnecessary repetition.

In this case, we may want to use our result from above in a second calculation. Instead of retyping 5 + 7 every time we need it, we can just create a new variable that stores the result.

To assign the result of 5 + 7 to a new variable called x, you type x <- 5 + 7. This can be read as 'x gets 5 plus 7'. Give it a try now.
```
x <- 5 + 7
```
To view the contents of the variable x, just type x and press Enter. Try it now.
```
x
```
Now, store the result of x - 3 in a new variable called y.
```
y <- x - 3
```
Now, let's create a small collection of numbers called a vector. Any object that contains data is called a data structure and numeric vectors are the simplest type of data structure in R. In fact, even a single number is considered a vector of length one.

The easiest way to create a vector is with the c() function, which stands for 'concatenate' or 'combine'. To create a vector containing the numbers 1.1, 9, and 3.14, type c(1.1, 9, 3.14). Try it now and store the result in a variable called z.
```
z <- c(1.1, 9, 3.14)
```
You can combine vectors to make a new vector. Create a new vector that contains z, 555, then z again in that order. Don't assign this vector to a new variable, so that we can just see the result immediately.
```
c(z, 555, z)
```
Numeric vectors can be used in arithmetic expressions. Type the following to see what happens: z * 2 + 100.
```
z * 2 + 100
```
Other common arithmetic operators are `+`, `-`, `/`, and `^` (where x^2 means 'x squared'). To take the square root, use the sqrt() function and to take the absolute value, use the abs() function.
Take the square root of z - 1 and assign it to a new variable called my_sqrt.
```
my_sqrt <- sqrt(z - 1)
```
Now, create a new variable called my_div that gets the value of z divided by my_sqrt.
```
my_div <- z / my_sqrt
```
When given two vectors of the same length, R simply performs the specified arithmetic operation (`+`, `-`, `*`, etc.) element-by-element. If the vectors are of different lengths, R 'recycles' the shorter vector until it is the same length as the longer vector.

When we did z * 2 + 100 in our earlier example, z was a vector of length 3, but technically 2 and 100 are each vectors of length 1.

Behind the scenes, R is 'recycling' the 2 to make a vector of 2s and the 100 to make a vector of 100s. In other words, when you ask R to compute z * 2 + 100, what it really computes is this: z * c(2, 2, 2) + c(100, 100, 100).

To see another example of how this vector 'recycling' works, try adding c(1, 2, 3, 4) and c(0, 10). Don't worry about saving the result in a new variable.
```
c(1, 2, 3, 4) + c(0, 10)
```
If the length of the shorter vector does not divide evenly into the length of the longer vector, R will still apply the 'recycling' method, but will throw a warning to let you know something fishy might be going on.

Try c(1, 2, 3, 4) + c(0, 10, 100) for an example.
```
c(1, 2, 3, 4) + c(0, 10, 100)
```
## 2. Workspace and Files
