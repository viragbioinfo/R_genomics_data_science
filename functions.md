Functions in R - inbuilt and customised
================
Virag Sharma

I have been using the word **function** for a while now without
explicitly mentioning what a function is. I would guess that you have
figured this out by now. But let us talk about functions in a more
formal way.

In terms of programming languages, a function is a piece of code that
lets you do an operation. In most of the cases, it will require an input
though it may not return an output every time you invoke a function. Let
us look at some in-built functions in R before we discuss how to write
your own functions.

## In-built functions in R

``` r
print('We are learning functions in this tutorial')
```

    ## [1] "We are learning functions in this tutorial"

As you have seen, I have called *print* which is our function and given
an input to it (basically the sentence ‘We are learning functions in
this tutorial’). Like any other function, the print function processes
the input and does the operation it is supposed to do, which in this
case is printing the sentence to the screen. Print is perhaps the
simplest function you can think of but there are more functions that you
use without even realizing that you have been using a function. More
examples will follow:

``` r
my_vector <- 1:3
my_names <- c('a', 'b', 'c')
names(my_vector) <- my_names
my_vector
```

    ## a b c 
    ## 1 2 3

We have seen before that we can potentially assign names to the elements
of a vector. But what helps us to do this? The function *names* which
receives an unnamed vector as an input.

``` r
my_pi = 22/7
round(my_pi)
```

    ## [1] 3

Now we make use of the round function to round-off the value of pi.

In addition, there are tons of functions and it is impossible to
remember the name of every function. However, R is such an intuitive
language that if you have been using R for a long time, you could even
guess the name of a function that will perform the operation you want to
do. Here are a couple of examples:

``` r
my_vector <- 1:10
mean(my_vector)
```

    ## [1] 5.5

``` r
median(my_vector)
```

    ## [1] 5.5

``` r
## Does not work, is not a valid function name
#stdev(my_vector)
## Works like a charm
sd(my_vector)
```

    ## [1] 3.02765

The functions – **mean** and **median** are extremely intuitive and it
is not hard to predict what they do. However, I really did not know the
name of the function to compute the standard deviation of a vector in R
but I tried with **stdev**, it did not work but I could confidently
guess then it must be **sd**, which turns out to be true.

## Writing your own custom functions in R

While you will benefit from most of the in-built functions that comes
with base R or with external packages that you will install, very often
you will need to come up with a function that is not available. This
means that you will need to write this function on your own.  
Let me also clarify that the point of writing a function is to avoid
writing the same block of code at several places in your script.
Functions also improve the readibility of your code as your code is
grouped into logical units. Let us look at an example:

``` r
x <- 1
y <- 1.5
my_sum <- x + y
cat('The sum of the numbers is ', my_sum, '\n')
```

    ## The sum of the numbers is  2.5

Here we have a block of code which computes the sum of two numbers and
prints a statement indicating the sum of the numbers. Now suppose we
want to do the same operation but different inputs. The corresponding
block of code will look like:

``` r
x1 <- 1.5
y1 <- 2.5
my_sum <- x1 + y1
cat('The sum of the numbers is ', my_sum, '\n')
```

    ## The sum of the numbers is  4

You see, we are writing the same code twice – compute sum and then the
print statement.  
Let us see how this can be bundled into a function

``` r
print_sum <- function(n1, n2) {
  my_sum = n1 + n2
  cat('The sum of the numbers is ', my_sum, '\n')
}

print_sum(1, 1.5)
```

    ## The sum of the numbers is  2.5

``` r
print_sum(1.5, 2.5)
```

    ## The sum of the numbers is  4

Here we have created a custom function called **print\_sum**. In terms
of syntax, the function has the following elements:  
1\. The name of the function – **print\_sum** in this case.  
2\. The assignment operator followed by the word *function* i.e. **\<-
function**.  
3\. A pair of brackets that contains the input arguments to the
function. In this case, these are two numbers/variables called n1 and
n2.  
4\. A pair of curly brackets which contains the body of the function
i.e. the code that performs the actual operation. In the above example,
the code is just two statements i.e computing the sum and printing the
sum but it is typically longer. In fact, this is the entire point of
writing a function. To encapsulate blocks of code together that perform
a task and keep them clear of the main body of the code.

#### Returning a value from a function

In the **print\_sum** function, we saw that the function accepts two
arguments, computes their sum and then prints the sum out. It does not
*return* a value back. This simply means that you do not get the value
of the sum back in another variable and hence you cannot access it. More
often than not, you will need to write a function that returns a value,
and this value could be used for further operations.

Everything remains the same as before, we just need to add a return
statement to the main body of the function.

``` r
return_sum <- function(n1, n2) {
  my_sum = n1 + n2
  return(my_sum)
}

s1 <- return_sum(1, 1.5)
s2 <- return_sum(1.5, 2.5)
cat('The sum of the first two numbers is', s1)
```

    ## The sum of the first two numbers is 2.5

``` r
cat('The sum next two numbers is', s2)
```

    ## The sum next two numbers is 4

``` r
sum_of_sums <- return_sum(s1, s2)
cat('The sum of all 4 numbers is', sum_of_sums)
```

    ## The sum of all 4 numbers is 6.5

So as you have seen now, we first define a *return\_sum* function that
takes two numbers as inputs, computes their sum and then **returns** the
value. The first time we call the function, we store the value of the
sum of two numbers - 1 and 1.5 in a variable called **s1**

The next time, we call the function, we store the value of the sum of
the two numbers - 1.5 and 2.5 in a variable called **s2**  
Since we have these values in variables now, which was not the case with
the print\_sum function because **it did not return any value**, we can
call the *return\_sum* function again on the the variables s1 and s2 and
compute their sum.
