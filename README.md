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
In this lesson, you'll learn how to examine your local workspace in R and begin to explore the relationship between your workspace and the file system of your machine.

Because different operating systems have different conventions with regards to things like file paths, the outputs of these commands may vary across machines.

However it's important to note that R provides a common API (a common set of commands) for interacting with files, that way your code will work across different kinds of computers.

Let's jump right in so you can get a feel for how these special functions work!

Determine which directory your R session is using as its current working directory using getwd().
```
getwd()
```
List all the objects in your local workspace using ls().
```
ls()
```
Assign 9 to x using x <- 9.
```
x <- 9
```
Now take a look at objects that are in your workspace using ls().
```
ls()
```
List all the files in your working directory using list.files() or dir().
```
list.files()
```
As we go through this lesson, you should be examining the help page for each new function. Check out the help page for list.files with the command ?list.files.
One of the most helpful parts of any R help file is the See Also section. Read that section for list.files. Some of these functions may be used in later portions of this lesson.

Using the args() function on a function name is also a handy way to see what arguments a function can take.

Use the args() function to determine the arguments to list.files().
```
args(list.files)
```
Assign the value of the current working directory to a variable called "old.dir".
```
old.dir <- getwd()
```
We will use old.dir at the end of this lesson to move back to the place that we started. A lot of query functions like getwd() have the useful property that they return the answer to the question as a result of the function.

Use dir.create() to create a directory in the current working directory called "testdir".
```
dir.create("testdir")
```
We will do all our work in this new directory and then delete it after we are done. This is the R analog to "Take only pictures, leave only footprints."

Set your working directory to "testdir" with the setwd() command.
```
setwd("testdir")
```
In general, you will want your working directory to be someplace sensible, perhaps created for the specific project that you are working on. In fact, organizing your work in R packages using RStudio is an excellent option. Check out RStudio at http://www.rstudio.com/

Create a file in your working directory called "mytest.R" using the file.create() function.
```
file.create("mytest.R")
```
This should be the only file in this newly created directory. Let's check this by listing all the files in the current directory.
```
list.files()
```
Check to see if "mytest.R" exists in the working directory using the file.exists() function.
```
file.exists("mytest.R")
```
These sorts of functions are excessive for interactive use. But, if you are running a program that loops through a series of files and does some processing on each one, you will want to check to see that each exists before you try to process it.

Access information about the file "mytest.R" by using file.info().
```
file.info("mytest.R")
```
You can use the $ operator --- e.g., file.info("mytest.R")$mode --- to grab specific items.

Change the name of the file "mytest.R" to "mytest2.R" by using file.rename().
```
file.rename("mytest.R", "mytest2.R")
```
Your operating system will provide simpler tools for these sorts of tasks, but having the ability to manipulate files programatically is useful. You might now try to delete mytest.R using file.remove('mytest.R'), but that won't work since mytest.R no longer exists. You have already renamed it.

Make a copy of "mytest2.R" called "mytest3.R" using file.copy().
```
file.copy("mytest2.R", "mytest3.R")
```
You now have two files in the current directory. That may not seem very interesting. But what if you were working with dozens, or millions, of individual files? In that case, being able to programatically act on many files would be absolutely necessary. Don't forget that you can, temporarily, leave the lesson by typing play() and then return by typing nxt().

Provide the relative path to the file "mytest3.R" by using file.path().
```
file.path("mytest3.R")
```
You can use file.path to construct file and directory paths that are independent of the operating system your R code is running on. Pass 'folder1' and 'folder2' as arguments to file.path to make a platform-independent pathname.
```
file.path("folder1", "folder2")
```
Take a look at the documentation for dir.create by entering ?dir.create . Notice the 'recursive' argument. In order to create nested directories, 'recursive' must be set to TRUE.

Create a directory in the current working directory called "testdir2" and a subdirectory for it called "testdir3", all in one command by using dir.create() and file.path().
```
dir.create(file.path("testdir2", "testdir3"), recursive = TRUE)
```
Go back to your original working directory using setwd(). (Recall that we created the variable old.dir with the full path for the orginal working directory at the start of these questions.)
```
setwd(old.dir)
```
It is often helpful to save the settings that you had before you began an analysis and then go back to them at the end. This trick is often used within functions; you save, say, the par() settings that you started with, mess around a bunch, and then set them back to the original values at the end. This isn't the same as what we have done here, but it seems similar enough to mention.

After you finish this lesson delete the 'testdir' directory that you just left (and everything in it)

Take nothing but results. Leave nothing but assumptions. That sounds like 'Take nothing but pictures. Leave nothing but footprints.' But it makes no sense! Surely our readers can come up with a better motto . . .

In this lesson, you learned how to examine your R workspace and work with the file system of your machine from within R. Thanks for playing!

## 3.Sequences of Numbers
In this lesson, you'll learn how to create sequences of numbers in R.

The simplest way to create a sequence of numbers in R is by using the `:` operator. Type 1:20 to see how it works.
```
1:20
```
That gave us every integer between (and including) 1 and 20. We could also use it to create a sequence of real numbers. For example, try pi:10.
```
pi:10
```
The result is a vector of real numbers starting with pi (3.142...) and increasing in increments of 1. The upper limit of 10 is never reached, since the next number in our sequence would be greater than 10.

What happens if we do 15:1? Give it a try to find out.
```
15:1
```
It counted backwards in increments of 1! It's unlikely we'd want this behavior, but nonetheless it's good to know how it could happen.

Remember that if you have questions about a particular R function, you can access its documentation with a question mark followed by the function name: ?function_name_here. However, in the case of an operator like the colon used above, you must enclose the symbol in backticks like this: ?':'. (NOTE: The backtick (') key is generally located in the top left corner of a keyboard, above the Tab key. If you don't have a backtick key, you can use regular quotes.)

Pull up the documentation for ':' now.
```
?':'
```
Often, we'll desire more control over a sequence we're creating than what the `:` operator gives us. The seq() function serves this purpose.

The most basic use of seq() does exactly the same thing as the `:` operator. Try seq(1, 20) to see this.
```
seq(1, 20)
```
This gives us the same output as 1:20. However, let's say that instead we want a vector of numbers ranging from 0 to 10, incremented by 0.5. seq(0, 10, by=0.5) does just that. Try it out.
```
seq(0, 10, by = 0.5)
```
Or maybe we don't care what the increment is and we just want a sequence of 30 numbers between 5 and 10. seq(5, 10, length=30) does the trick. Give it a shot now and store the result in a new variable called my_seq.
```
my_seq <- seq(5, 10, length = 30)
```
To confirm that my_seq has length 30, we can use the length() function. Try it now.
```
length(my_seq)
```
Let's pretend we don't know the length of my_seq, but we want to generate a sequence of integers from 1 to N, where N represents the length of the my_seq vector. In other words, we want a new vector (1, 2, 3, ...) that is the same length as my_seq.

There are several ways we could do this. One possibility is to combine the `:` operator and the length() function like this: 1:length(my_seq). Give that a try.
```
1:length(my_seq)
```
Another option is to use seq(along.with = my_seq). Give that a try.
```
seq(along.with = my_seq)
```
However, as is the case with many common tasks, R has a separate built-in function for this purpose called seq_along(). Type seq_along(my_seq) to see it in action.
```
seq(along.with = my_seq)
```
However, as is the case with many common tasks, R has a separate built-in function for this purpose called seq_along(). Type seq_along(my_seq) to see it in action.
```
seq_along(my_seq)
```
There are often several approaches to solving the same problem, particularly in R. Simple approaches that involve less typing are generally best. It's also important for your code to be readable, so that you and others can figure out what's going on without too much hassle.

If R has a built-in function for a particular task, it's likely that function is highly optimized for that purpose and is your best option. As you become a more advanced R programmer, you'll design your own functions to perform tasks when there are no better options. We'll explore writing your own functions in future lessons.

One more function related to creating sequences of numbers is rep(), which stands for 'replicate'. Let's look at a few uses.

If we're interested in creating a vector that contains 40 zeros, we can use rep(0, times = 40). Try it out.
```
rep(0, times = 40)
```
If instead we want our vector to contain 10 repetitions of the vector (0, 1, 2), we can do rep(c(0, 1, 2), times = 10). Go ahead.
```
rep(c(0, 1, 2), times = 10)
```
Finally, let's say that rather than repeating the vector (0, 1, 2) over and over again, we want our vector to contain 10 zeros, then 10 ones, then 10 twos. We can do this with the `each` argument. Try rep(c(0, 1, 2), each = 10).
```
rep(c(0, 1, 2), each = 10)
```
## 4. Vectors
The simplest and most common data structure in R is the vector.

Vectors come in two different flavors: atomic vectors and lists. An atomic vector contains exactly one data type, whereas a list may contain multiple data types. We'll explore atomic vectors further before we get to lists.

In previous lessons, we dealt entirely with numeric vectors, which are one type of atomic vector. Other types of atomic vectors include logical, character, integer, and complex. In this lesson, we'll take a closer look at logical and character vectors.

Logical vectors can contain the values TRUE, FALSE, and NA (for 'not available'). These values are generated as the result of logical 'conditions'. Let's experiment with some simple conditions.

First, create a numeric vector num_vect that contains the values 0.5, 55, -10, and 6.
```
num_vect <- c(0.5, 55, -10, 6)
```
Now, create a variable called tf that gets the result of num_vect < 1, which is read as 'num_vect is less than 1'.
```
tf <- num_vect<1
```
tf will look like a vector of 4 logical values.
Print the contents of tf now.
```
tf
```
The statement num_vect < 1 is a condition and tf tells us whether each corresponding element of our numeric vector num_vect satisfies this condition.

The first element of num_vect is 0.5, which is less than 1 and therefore the statement 0.5 < 1 is TRUE. The second element of num_vect is 55, which is greater than 1, so the statement 55 < 1 is FALSE. The same logic applies for the third and fourth elements.

Let's try another. Type num_vect >= 6 without assigning the result to a new variable.
```
num_vect >= 6
```
This time, we are asking whether each individual element of num_vect is greater than OR equal to 6. Since only 55 and 6 are greater than or equal to 6, the second and fourth elements of the result are TRUE and the first and third elements are FALSE.

The `<` and `>=` symbols in these examples are called 'logical operators'. Other logical operators include `>`, `<=`, `==` for exact equality, and `!=` for inequality.

If we have two logical expressions, A and B, we can ask whether at least one is TRUE with A | B (logical 'or' a.k.a. 'union') or whether they are both TRUE with A & B (logical 'and' a.k.a. 'intersection'). Lastly, !A is the negation of A and is TRUE when A is FALSE and vice versa.

It's a good idea to spend some time playing around with various combinations of these logical operators until you get comfortable with their use. We'll do a few examples here to get you started.

(3 > 5) & (4 == 4) FALSE

(TRUE == TRUE) | (TRUE == FALSE) TRUE

((111 >= 111) | !(TRUE)) & ((4 + 1) == 5) TRUE
Character vectors are also very common in R. Double quotes are used to distinguish character objects, as in the following example.

Create a character vector that contains the following words: "My", "name", "is". Remember to enclose each word in its own set of double quotes, so that R knows they are character strings. Store the vector in a variable called my_char.
```
my_char <- c("My", "name", "is")
```
Print the contents of my_char to see what it looks like.
```
my_char
```
Right now, my_char is a character vector of length 3. Let's say we want to join the elements of my_char together into one continuous character string (i.e. a character vector of length 1). We can do this using the paste() function.

Type paste(my_char, collapse = " ") now. Make sure there's a space between the double quotes in the `collapse` argument. You'll see why in a second.
```
paste(my_char, collapse = " ")
```
To add (or 'concatenate') your name to the end of my_char, use the c() function like this: c(my_char, "your_name_here"). Place your name in double quotes where I've put "your_name_here". Try it now, storing the result in a new variable called my_name.
```
my_name <- c(my_char, "Jiahui")
```
Now, use the paste() function once more to join the words in my_name together into a single character string. Don't forget to say collapse = " "!
```
paste(my_name, collapse = " ")
```
In this example, we used the paste() function to collapse the elements of a single character vector. paste() can also be used to join the elements of multiple character vectors.

In the simplest case, we can join two character vectors that are each of length 1 (i.e. join two words). Try paste("Hello", "world!", sep = " "), where the `sep` argument tells R that we want to separate the joined elements with a single space.
```
paste("Hello", "world!", sep = " ")
```
For a slightly more complicated example, we can join two vectors, each of length 3. Use paste() to join the integer vector 1:3 with the character vector c("X", "Y", "Z"). This time, use sep = "" to leave no space between the joined elements.
```
paste(1:3, c("X", "Y", "Z"), sep = "")
```
What do you think will happen if our vectors are of different length? (Hint: we talked about this in a previous lesson.)

Vector recycling! Try paste(LETTERS, 1:4, sep = "-"), where LETTERS is a predefined variable in R containing a character vector of all 26 letters in the English alphabet.
```
paste(LETTERS, 1:4, sep = "-")
```
Since the character vector LETTERS is longer than the numeric vector 1:4, R simply recycles, or repeats, 1:4 until it matches the length of LETTERS.

Also worth noting is that the numeric vector 1:4 gets 'coerced' into a character vector by the paste() function.

We'll discuss coercion in another lesson, but all it really means is that the numbers 1, 2, 3, and 4 in the output above are no longer numbers to R, but rather characters "1", "2", "3", and "4".

## 5. Missing Values
Missing values play an important role in statistics and data analysis. Often, missing values must not be ignored, but rather they should be carefully studied to see if there's an underlying pattern or cause for their missingness.

In R, NA is used to represent any value that is 'not available' or 'missing' (in the statistical sense). In this lesson, we'll explore missing values further.

Any operation involving NA generally yields NA as the result. To illustrate, let's create a vector c(44, NA, 5, NA) and assign it to a variable x.
```
x <- c(44, NA, 5, NA)
```
Now, let's multiply x by 3.
```
x*3
```
Notice that the elements of the resulting vector that correspond with the NA values in x are also NA.

To make things a little more interesting, lets create a vector containing 1000 draws from a standard normal distribution with y <- rnorm(1000).
```
y <- rnorm(1000)
```
Next, let's create a vector containing 1000 NAs with z <- rep(NA, 1000).
```
z <- rep(NA, 1000)
```
Finally, let's select 100 elements at random from these 2000 values (combining y and z) such that we don't know how many NAs we'll wind up with or what positions they'll occupy in our final vector -- my_data <- sample(c(y, z), 100).
```
my_na <- is.na(my_data)
```
Now, print my_na to see what you came up with.
```
my_na
```
Everywhere you see a TRUE, you know the corresponding element of my_data is NA. Likewise, everywhere you see a FALSE, you know the corresponding element of my_data is one of our random draws from the standard normal distribution.

In our previous discussion of logical operators, we introduced the `==` operator as a method of testing for equality between two objects. So, you might think the expression my_data == NA yields the same results as is.na(). Give it a try.
```
my_data == NA
```
The reason you got a vector of all NAs is that NA is not really a value, but just a placeholder for a quantity that is not available. Therefore the logical expression is incomplete and R has no choice but to return a vector of the same length as my_data that contains all NAs.

Don't worry if that's a little confusing. The key takeaway is to be cautious when using logical expressions anytime NAs might creep in, since a single NA value can derail the entire thing.

So, back to the task at hand. Now that we have a vector, my_na, that has a TRUE for every NA and FALSE for every numeric value, we can compute the total number of NAs in our data.

The trick is to recognize that underneath the surface, R represents TRUE as the number 1 and FALSE as the number 0. Therefore, if we take the sum of a bunch of TRUEs and FALSEs, we get the total number of TRUEs.

Let's give that a try here. Call the sum() function on my_na to count the total number of TRUEs in my_na, and thus the total number of NAs in my_data. Don't assign the result to a new variable.
```
sum(my_na)
```
Pretty cool, huh? Finally, let's take a look at the data to convince ourselves that everything 'adds up'. Print my_data to the console.
```
my_data
```
Now that we've got NAs down pat, let's look at a second type of missing value -- NaN, which stands for 'not a number'. To generate NaN, try dividing (using a forward slash) 0 by 0 now.
```
0 / 0
[1] NaN
```
Let's do one more, just for fun. In R, Inf stands for infinity. What happens if you subtract Inf from Inf?
```
Inf - Inf
```

## 6. Subsetting Vectors
In this lesson, we'll see how to extract elements from a vector based on some conditions that we specify.

For example, we may only be interested in the first 20 elements of a vector, or only the elements that are not NA, or only those that are positive or correspond to a specific variable of interest. By the end of this lesson, you'll know how to handle each of these scenarios.

I've created for you a vector called x that contains a random ordering of 20 numbers (from a standard normal distribution) and 20 NAs. Type x now to see what it looks like.
```
x
```
The way you tell R that you want to select some particular elements (i.e. a 'subset') from a vector is by placing an 'index vector' in square brackets immediately following the name of the vector.

For a simple example, try x[1:10] to view the first ten elements of x.
```
x[1:10]
```
Index vectors come in four different flavors -- logical vectors, vectors of positive integers, vectors of negative integers, and vectors of character strings -- each of which we'll cover in this lesson.

Let's start by indexing with logical vectors. One common scenario when working with real-world data is that we want to extract all elements of a vector that are not NA (i.e. missing data). Recall that is.na(x) yields a vector of logical values the same length as x, with TRUEs corresponding to NA values in x and FALSEs corresponding to non-NA values in x.

x[is.na(x)] will give you a vector of all NAs.

Recall that `!` gives us the negation of a logical expression, so !is.na(x) can be read as 'is not NA'. Therefore, if we want to create a vector called y that contains all of the non-NA values from x, we can use y <- x[!is.na(x)]. Give it a try.
```
y <- x[!is.na(x)]
```
Now that we've isolated the non-missing values of x and put them in y, we can subset y as we please.

Recall that the expression y > 0 will give us a vector of logical values the same length as y, with TRUEs corresponding to values of y that are greater than zero and FALSEs corresponding to values of y that are less than or equal to zero. What do you think y[y > 0] will give you? A vector of all the positive elements of y.

Type y[y > 0] to see that we get all of the positive elements of y, which are also the positive elements of our original vector x.
```
y[y > 0]
```
You might wonder why we didn't just start with x[x > 0] to isolate the positive elements of x. Try that now to see why.
```
x[x > 0]
```
Since NA is not a value, but rather a placeholder for an unknown quantity, the expression NA > 0 evaluates to NA. Hence we get a bunch of NAs mixed in with our positive numbers when we do this.

Combining our knowledge of logical operators with our new knowledge of subsetting, we could do this -- x[!is.na(x) & x > 0]. Try it out.
```
x[!is.na(x) & x > 0]
```
In this case, we request only values of x that are both non-missing AND greater than zero.

I've already shown you how to subset just the first ten values of x using x[1:10]. In this case, we're providing a vector of positive integers inside of the square brackets, which tells R to return only the elements of x numbered 1 through 10.

Many programming languages use what's called 'zero-based indexing', which means that the first element of a vector is considered element 0. R uses 'one-based indexing', which (you guessed it!) means the first element of a vector is considered element 1.

Can you figure out how we'd subset the 3rd, 5th, and 7th elements of x? Hint -- Use the c() function to specify the element numbers as a numeric vector.
```
x[c(3, 5, 7)]
```
It's important that when using integer vectors to subset our vector x, we stick with the set of indexes {1, 2, ..., 40} since x only has 40 elements. What happens if we ask for the zeroth element of x (i.e. x[0])? Give it a try.
```
x[0]
```
As you might expect, we get nothing useful. Unfortunately, R doesn't prevent us from doing this. What if we ask for the 3000th element of x? Try it out.
```
x[3000]
```
Again, nothing useful, but R doesn't prevent us from asking for it. This should be a cautionary tale. You should always make sure that what you are asking for is within the bounds of the vector you're working with.

What if we're interested in all elements of x EXCEPT the 2nd and 10th? It would be pretty tedious to construct a vector containing all numbers 1 through 40 EXCEPT 2 and 10.

Luckily, R accepts negative integer indexes. Whereas x[c(2, 10)] gives us ONLY the 2nd and 10th elements of x, x[c(-2, -10)] gives us all elements of x EXCEPT for the 2nd and 10 elements.  Try x[c(-2, -10)] now to see this.
```
x[c(-2, -10)]
```
A shorthand way of specifying multiple negative numbers is to put the negative sign out in front of the vector of positive numbers. Type x[-c(2, 10)] to get the exact same result.
```
x[-c(2, 10)]
```
So far, we've covered three types of index vectors -- logical, positive integer, and negative integer. The only remaining type requires us to introduce the concept of 'named' elements.

Create a numeric vector with three named elements using vect <- c(foo = 11, bar = 2, norf = NA).
```
vect <- c(foo = 11, bar = 2, norf = NA)
```
When we print vect to the console, you'll see that each element has a name. Try it out.
```
vect
```
We can also get the names of vect by passing vect as an argument to the names() function. Give that a try.
```
names(vect)
```
Alternatively, we can create an unnamed vector vect2 with c(11, 2, NA). Do that now.
```
vect2 <- c(11, 2, NA)
```
Then, we can add the `names` attribute to vect2 after the fact with names(vect2) <- c("foo", "bar", "norf"). Go ahead.
```
names(vect2) <- c("foo", "bar","norf")
```
Now, let's check that vect and vect2 are the same by passing them as arguments to the identical() function.
```
identical(vect, vect2)
```

Indeed, vect and vect2 are identical named vectors.

Now, back to the matter of subsetting a vector by named elements. Which of the following commands do you think would give us the second element of vect? vect["bar"]

Likewise, we can specify a vector of names with vect[c("foo", "bar")]. Try it out.
```
vect[c("foo", "bar")]
```
Now you know all four methods of subsetting data from vectors. Different approaches are best in different scenarios and when in doubt, try it out!
