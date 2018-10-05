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
