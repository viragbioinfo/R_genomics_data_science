while Loop
================
Virag Sharma

Now that we have learnt about the *for* loop, we are going to learn
about the *while*.  
The *while* loop is similar to the *for* loop because it allows looping,
pretty much like the *for* loop. As a result, we can continue to execute
a block of code until the condition that we are testing is met.

Before we look at the the *while* loop in action, it would be useful to
check the *cat* function in R.

### Detour - *cat* function

Suppose we have a numeric object called *x* and we assign a value of 10
to it. To print the value of *x* in our console, we simply type the
object name and we can retrieve its value.

``` r
x <- 10
x
```

    ## [1] 10

Now suppose we want to prefix some text before we print the value of
*x*. If we want to print \*\* Our variable x has the value 10\*\*, then
we can make use of the *cat* function.

``` r
cat("Our variable x has the value", x)
```

    ## Our variable x has the value 10

This prints the desired statement. As you can see, the usage of the
*cat* function is pretty simple. We basically concatenate our text and
our variable and separate the two by commas i.e. **“,”**.

We could use the same function to concatenate more than one
variable/text. See below:

``` r
x <- 10
y <- 20
cat ("Our variable x has the value of ", x, "while our variable y has the value of", y)
```

    ## Our variable x has the value of  10 while our variable y has the value of 20

## While loop

Now that we have learnt how to print some text/object combination
together in R, let us look at the *while loop*. As stated earlier, the
*while* loop allows us to continue executing some code/operation until
the condition that we are testing returns **TRUE**.

``` r
i <- 1
while (i <= 10) {
  cat('The value of our variable i is', i, '\n')
  i <- i + 1
}
```

    ## The value of our variable i is 1 
    ## The value of our variable i is 2 
    ## The value of our variable i is 3 
    ## The value of our variable i is 4 
    ## The value of our variable i is 5 
    ## The value of our variable i is 6 
    ## The value of our variable i is 7 
    ## The value of our variable i is 8 
    ## The value of our variable i is 9 
    ## The value of our variable i is 10

The syntax is very similar to the *if* statement or the *for* loop, that
we have seen before. 1. There is the *while* keyword followed by the
condition we are testing. In the above example, we are testing if i is
less than or equal to 10. So basically, this condition will keep failing
i.e. returning **FALSE** unless our variable becomes greater than 10.  
2\. Secondly, we have a pair of braces and within this, we are doing not
much other than printing the current value of *i*. However, the most
important part of this *while* loop is that we are incrementing the
value of *i* by 1 at every iteration. If we do not do this, then you
will end up with an infinite loop because you keep testing if *i* has
become greater than 10 but *i* remains stuck at the value we had
assigned before the beginning of the *while* loop.

Let us look at another example where we will use the *while* loop to
print all even numbers from 2 till 10

``` r
i <- 2
while (i <= 10) {
  cat('The value of our variable i is', i, '\n')
  i <- i + 2
}
```

    ## The value of our variable i is 2 
    ## The value of our variable i is 4 
    ## The value of our variable i is 6 
    ## The value of our variable i is 8 
    ## The value of our variable i is 10

Similarly, if we want to print the odd numbers between 1 till 10, we
need to start at 1.

``` r
i <- 1
while (i <= 10) {
  cat('The value of our variable i is', i, '\n')
  i <- i + 2
}
```

    ## The value of our variable i is 1 
    ## The value of our variable i is 3 
    ## The value of our variable i is 5 
    ## The value of our variable i is 7 
    ## The value of our variable i is 9
