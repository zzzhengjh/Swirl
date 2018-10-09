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

## 7. Matrices and Data Frames
In this lesson, we'll cover matrices and data frames. Both represent 'rectangular' data types, meaning that they are used to store tabular data, with rows and columns.

The main difference, as you'll see, is that matrices can only contain a single class of data, while data frames can consist of many different classes of data.

Let's create a vector containing the numbers 1 through 20 using the `:` operator. Store the result in a variable called my_vector.
```
my_vector <- 1:20
```
The dim() function tells us the 'dimensions' of an object. What happens if we do dim(my_vector)? Give it a try.
```
dim(my_vector)
```
Clearly, that's not very helpful! Since my_vector is a vector, it doesn't have a `dim` attribute (so it's just NULL), but we can find its length using the length() function. Try that now.
```
length(my_vector)
```
Ah! That's what we wanted. But, what happens if we give my_vector a `dim` attribute? Let's give it a try. Type dim(my_vector) <- c(4, 5).
```
dim(my_vector) <- c(4, 5)
```
It's okay if that last command seemed a little strange to you. It should! The dim() function allows you to get OR set the `dim` attribute for an R object. In this case, we assigned the value c(4, 5) to the `dim` attribute of my_vector.

Use dim(my_vector) to confirm that we've set the `dim` attribute correctly.
```
dim(my_vector)
```
Another way to see this is by calling the attributes() function on my_vector. Try it now.
```
attributes(my_vector)
```
Just like in math class, when dealing with a 2-dimensional object (think rectangular table), the first number is the number of rows and the second is the number of columns. Therefore, we just gave my_vector 4 rows and 5 columns.

But, wait! That doesn't sound like a vector any more. Well, it's not. Now it's a matrix. View the contents of my_vector now to see what it looks like.
```
my_vector
```
Now, let's confirm it's actually a matrix by using the class() function. Type class(my_vector) to see what I mean.
```
class(my_vector)
```
Sure enough, my_vector is now a matrix. We should store it in a new variable that helps us remember what it is. Store the value of my_vector in a new variable called my_matrix.
```
my_matrix <- my_vector
```
The example that we've used so far was meant to illustrate the point that a matrix is simply an atomic vector with a dimension attribute. A more direct method of creating the same matrix uses the matrix() function.

Now, look at the documentation for the matrix function and see if you can figure out how to create a matrix containing the same numbers (1-20) and dimensions (4 rows, 5 columns) by calling the matrix() function. Store the result in a variable called my_matrix2.
```
my_matrix2 <- matrix(1:20, nrow = 4, ncol = 5)
```
Finally, let's confirm that my_matrix and my_matrix2 are actually identical. The identical() function will tell us if its first two arguments are the same. Try it out.
```
identical(my_matrix, my_matrix2)
```
Now, imagine that the numbers in our table represent some measurements from a clinical experiment, where each row represents one patient and each column represents one variable for which measurements were taken.

We may want to label the rows, so that we know which numbers belong to each patient in the experiment. One way to do this is to add a column to the matrix, which contains the names of all four people.

Let's start by creating a character vector containing the names of our patients -- Bill, Gina, Kelly, and Sean. Remember that double quotes tell R that something is a character string. Store the result in a variable called patients.
```
patients <- c("Bill", "Gina", "Kelly", "Sean")
```
Now we'll use the cbind() function to 'combine columns'. Don't worry about storing the result in a new variable. Just call cbind() with two arguments -- the patients vector and my_matrix.
```
cbind(patients, my_matrix)
```
Something is fishy about our result! It appears that combining the character vector with our matrix of numbers caused everything to be enclosed in double quotes. This means we're left with a matrix of character strings, which is no good.

If you remember back to the beginning of this lesson, I told you that matrices can only contain ONE class of data. Therefore, when we tried to combine a character vector with a numeric matrix, R was forced to 'coerce' the numbers to characters, hence the double quotes.

This is called 'implicit coercion', because we didn't ask for it. It just happened. But why didn't R just convert the names of our patients to numbers? I'll let you ponder that question on your own.

So, we're still left with the question of how to include the names of our patients in the table without destroying the integrity of our numeric data. Try the following -- my_data <- data.frame(patients, my_matrix)
```
my_data <- data.frame(patients, my_matrix)
```
Now view the contents of my_data to see what we've come up with.
```
my_data
```
It looks like the data.frame() function allowed us to store our character vector of names right alongside our matrix of numbers. That's exactly what we were hoping for!

Behind the scenes, the data.frame() function takes any number of arguments and returns a single object of class `data.frame` that is composed of the original objects.

Let's confirm this by calling the class() function on our newly created data frame.
```
class(my_data)
```
It's also possible to assign names to the individual rows and columns of a data frame, which presents another possible way of determining which row of values in our table belongs to each patient.

However, since we've already solved that problem, let's solve a different problem by assigning names to the columns of our data frame so that we know what type of measurement each column represents.

Since we have six columns (including patient names), we'll need to first create a vector containing one element for each column. Create a character vector called cnames that contains the following values (in order) -- "patient", "age", "weight", "bp", "rating", "test".
```
cnames <- c("patient", "age", "weight", "bp", "rating", "test")
```
Now, use the colnames() function to set the `colnames` attribute for our data frame. This is similar to the way we used the dim() function earlier in this lesson.
```
colnames(my_data) <- cnames
```
Let's see if that got the job done. Print the contents of my_data.
```
my_data
```
In this lesson, you learned the basics of working with two very important and common data structures -- matrices and data frames. There's much more to learn and we'll be covering more advanced topics, particularly with respect to data frames, in future lessons.

## 8. Logic
This lesson is meant to be a short introduction to logical operations in R.

There are two logical values in R, also called boolean values. They are TRUE and FALSE. In R you can construct logical expressions which will evaluate to either TRUE or FALSE.

Many of the questions in this lesson will involve evaluating logical expressions. It may be useful to open up a second R terminal where you can experiment with some of these expressions.

Creating logical expressions requires logical operators. You're probably familiar with arithmetic operators like `+`, `-`, `*`, and `/`. The first logical operator we are going to discuss is the equality operator, represented by two equals signs `==`. Use the equality operator below to find out if TRUE is equal to TRUE.
```
TRUE == TRUE
```
Just like arithmetic, logical expressions can be grouped by parenthesis so that the entire expression (TRUE == TRUE) == TRUE evaluates to TRUE.

To test out this property, try evaluating (FALSE == TRUE) == FALSE .
```
(FALSE == TRUE) == FALSE
```
The equality operator can also be used to compare numbers. Use `==` to see if 6 is equal to 7.
```
6 == 7
```
The previous expression evaluates to FALSE because 6 is less than 7. Thankfully, there are inequality operators that allow us to test if a value is less than or greater than another value.

The less than operator `<` tests whether the number on the left side of the operator (called the left operand) is less than the number on the right side of the operator (called the right operand). Write an expression to test whether 6 is less than 7.
```
6 < 7
```
There is also a less-than-or-equal-to operator `<=` which tests whether the left operand is less than or equal to the right operand. Write an expression to test whether 10 is less than or equal to 10.
```
10 <= 10
```
Keep in mind that there are the corresponding greater than `>` and greater-than-or-equal-to `>=` operators.

Which of the following evaluates to FALSE?

1: 0 > -36
2: 6 < 8
3: 9 >= 10
4: 7 == 7

Selection: 3

Which of the following evaluates to TRUE?

1: 7 == 9
2: -6 > -7
3: 9 >= 10
4: 57 < 8

Selection: 2

The next operator we will discuss is the 'not equals' operator represented by `!=`. Not equals tests whether two values are unequal, so TRUE != FALSE evaluates to TRUE. Like the equality operator, `!=` can also be used with numbers. Try writing an expression to see if 5 is not equal to 7.
```
5 != 7
```
In order to negate boolean expressions you can use the NOT operator. An exclamation point `!` will cause !TRUE (say: not true) to evaluate to FALSE and !FALSE (say: not false) to evaluate to TRUE. Try using the NOT operator and the equals operator to find the opposite of whether 5 is equal to 7.
```
! 5 == 7
```
Let's take a moment to review. The equals operator `==` tests whether two boolean values or numbers are equal, the not equals operator `!=` tests whether two boolean values or numbers are unequal, and the NOT operator `!` negates logical expressions so that TRUE expressions become FALSE and FALSE expressions become TRUE.

Which of the following evaluates to FALSE?

1: !FALSE
2: 9 < 10
3: 7 != 8
4: !(0 >= -1)

Selection: 4

What do you think the following expression will evaluate to?: (TRUE != FALSE) == !(6 == 7)

1: TRUE
2: FALSE
3: %>%
4: Can there be objective truth when programming?

Selection: 1

At some point you may need to examine relationships between multiple logical expressions. This is where the AND operator and the OR operator come in.

Let's look at how the AND operator works. There are two AND operators in R, `&` and `&&`. Both operators work similarly, if the right and left operands of AND are both TRUE the entire expression is TRUE, otherwise it is FALSE. For example, TRUE & TRUE evaluates to TRUE. Try typing FALSE & FALSE to how it is evaluated.
```
FALSE & FALSE
```
You can use the `&` operator to evaluate AND across a vector. The `&&` version of AND only evaluates the first member of a vector. Let's test both for practice. Type the expression TRUE & c(TRUE, FALSE, FALSE).
```
TRUE & c(TRUE, FALSE, FALSE)
```
What happens in this case is that the left operand `TRUE` is recycled across every element in the vector of the right operand. This is the equivalent statement as c(TRUE, TRUE, TRUE) & c(TRUE, FALSE, FALSE).

Now we'll type the same expression except we'll use the `&&` operator. Type the expression TRUE && c(TRUE, FALSE, FALSE).
```
TRUE && c(TRUE, FALSE, FALSE)
```
In this case, the left operand is only evaluated with the first member of the right operand (the vector). The rest of the elements in the vector aren't evaluated at all in this expression.

The OR operator follows a similar set of rules. The `|` version of OR evaluates OR across an entire vector, while the `||` version of OR only evaluates the first member of a vector.

An expression using the OR operator will evaluate to TRUE if the left operand or the right operand is TRUE. If both are TRUE, the expression will evaluate to TRUE, however if neither are TRUE, then the expression will be FALSE.

Let's test out the vectorized version of the OR operator. Type the expression TRUE | c(TRUE, FALSE, FALSE).
```
TRUE | c(TRUE, FALSE, FALSE)
```
Now let's try out the non-vectorized version of the OR operator. Type the expression TRUE || c(TRUE, FALSE, FALSE).
```
TRUE || c(TRUE, FALSE, FALSE)
```
Logical operators can be chained together just like arithmetic operators. The expressions: `6 != 10 && FALSE && 1 >= 2` or `TRUE || 5 < 9.3 || FALSE` are perfectly normal to see.

As you may recall, arithmetic has an order of operations and so do logical expressions. All AND operators are evaluated before OR operators. Let's look at an example of an ambiguous case. Type: 5 > 8 || 6 != 8 && 4 > 3.9
```
5 > 8 || 6 != 8 && 4 > 3.9
```
Let's walk through the order of operations in the above case. First the left and right operands of the AND operator are evaluated. 6 is not equal 8, 4 is greater than 3.9, therefore both operands are TRUE so the resulting expression `TRUE && TRUE` evaluates to TRUE. Then the left operand of the OR operator is evaluated: 5 is not greater than 8 so the entire expression is reduced to FALSE || TRUE. Since the right operand of this expression is TRUE the entire expression evaluates to TRUE.

Which one of the following expressions evaluates to TRUE?

1: 99.99 > 100 || 45 < 7.3 || 4 != 4.0
2: TRUE && 62 < 62 && 44 >= 44
3: FALSE || TRUE && FALSE
4: TRUE && FALSE || 9 >= 4 && 3 < 6

Selection: 4

Which one of the following expressions evaluates to FALSE?

1: FALSE || TRUE && 6 != 4 || 9 > 4
2: !(8 > 4) ||  5 == 5.0 && 7.8 >= 7.79
3: 6 >= -9 && !(6 > 7) && !(!TRUE)
4: FALSE && 6 >= 6 || 7 >= 8 || 50 <= 49.5

Selection: 4

Now that you're familiar with R's logical operators you can take advantage of a few functions that R provides for dealing with logical expressions.

The function isTRUE() takes one argument. If that argument evaluates to TRUE, the function will return TRUE. Otherwise, the function will return FALSE. Try using this function by typing: isTRUE(6 > 4)
```
isTRUE(6 > 4)
```
Which of the following evaluates to TRUE?

1: isTRUE(NA)
2: isTRUE(!TRUE)
3: !isTRUE(4 < 3)
4: isTRUE(3)
5: !isTRUE(8 != 5)

Selection: 3

The function identical() will return TRUE if the two R objects passed to it as arguments are identical. Try out the identical() function by typing: identical('twins', 'twins')
```
identical('twins', 'twins')
```
Which of the following evaluates to TRUE?

1: identical(5 > 4, 3 < 3.1)
2: identical('hello', 'Hello')
3: identical(4, 3.1)
4: !identical(7, 7)

Selection: 1

You should also be aware of the xor() function, which takes two arguments. The xor() function stands for exclusive OR. If one argument evaluates to TRUE and one argument evaluates to FALSE, then this function will return TRUE, otherwise it will return FALSE. Try out the xor() function by typing: xor(5 == 6, !FALSE)
```
xor(5 == 6, !FALSE)
```
5 == 6 evaluates to FALSE, !FALSE evaluates to TRUE, so xor(FALSE, TRUE) evaluates to TRUE. On the other hand if the first argument was changed to 5 == 5 and the second argument was unchanged then both arguments would have been TRUE, so xor(TRUE, TRUE) would have evaluated to FALSE.

Which of the following evaluates to FALSE?

1: xor(identical(xor, 'xor'), 7 == 7.0)
2: xor(!!TRUE, !!FALSE)
3: xor(!isTRUE(TRUE), 6 > -1)
4: xor(4 >= 9, 8 != 8.0)

Selection: 4

For the next few questions, we're going to need to create a vector of integers called ints. Create this vector by typing: ints <- sample(10)
```
ints <- sample(10)
```
Now simply display the contents of ints.
```
ints
```
The vector `ints` is a random sampling of integers from 1 to 10 without replacement. Let's say we wanted to ask some logical questions about contents of ints. If we type ints > 5, we will get a logical vector corresponding to whether each element of ints is greater than 5. Try typing: ints > 5
```
ints >5
```
We can use the resulting logical vector to ask other questions about ints. The which() function takes a logical vector as an argument and returns the indices of the vector that are TRUE. For example which(c(TRUE, FALSE, TRUE)) would return the vector c(1, 3).

Use the which() function to find the indices of ints that are greater than 7.
```
which(ints > 7)
```
Which of the following commands would produce the indices of the elements in ints that are less than or equal to 2?

1: ints < 2
2: which(ints <= 2)
3: which(ints < 2)
4: ints <= 2

Selection: 2

Like the which() function, the functions any() and all() take logical vectors as their argument. The any() function will return TRUE if one or more of the elements in the logical vector is TRUE. The all() function will return TRUE if every element in the logical vector is TRUE.

Use the any() function to see if any of the elements of ints are less than zero.
```
any(ints < 0)
```
Use the all() function to see if all of the elements of ints are greater than zero.
```
> all(ints > 0)
```
Which of the following evaluates to TRUE?

1: any(ints == 2.5)
2: all(ints == 10)
3: any(ints == 10)
4: all(c(TRUE, FALSE, TRUE))

Selection: 3

That's all for this introduction to logic in R. If you really want to see what you can do with logic, check out the control flow lesson!
