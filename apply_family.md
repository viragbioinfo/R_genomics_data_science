lapply and sapply: Part 1
================
Virag Sharma

In this tutorial, we are going to learn about the family of **apply**
functions. The two commonly used functions that you will come across as
you write and read R-code are the following:  
1\. lapply  
2\. sapply

Let us look at some examples to see how they work.

``` r
my_vector <- 1:5

add_one <- function(number) {
  return(number + 1)
}

my_vector_lapply <- lapply(my_vector, add_one)
my_vector_lapply
```

    ## [[1]]
    ## [1] 2
    ## 
    ## [[2]]
    ## [1] 3
    ## 
    ## [[3]]
    ## [1] 4
    ## 
    ## [[4]]
    ## [1] 5
    ## 
    ## [[5]]
    ## [1] 6

Wow\!\! what was that. Let us break this down into individual steps:  
1\. First, we defined a vetor that contains numbers from 1 till 5.  
2\. Secondly, we defined a custom function called **add\_one** that
takes a number as an input, add 1 to this input and then return the
incremented value.  
3\. Then we run the **lapply function** with two arguments – the first
one is our vector, the second is our custom function i.e add\_one, and
store the output in an object called *my\_vector\_lapply*.  
4\. Lastly, we print the object *my\_vector\_lapply*.

What we see is that as we called *lapply* on a vector (*my\_vector*) and
a function(*add\_one*), every element in our vector got incremented by
1. Interestingly, the output was returned in the form of a list. This
can also be confirmed by asking if the output is a list:

``` r
is.list(my_vector_lapply)
```

    ## [1] TRUE

While lists can be useful as objects, we do not really make use of lists
unless we really want to mix different objects together. Instead, we
could benefit from a friendlier object such as a vector. The function
sapply does precisely this.  
Let us see **sapply** in action now:

``` r
my_vector_sapply <- sapply(my_vector, add_one)
my_vector_sapply
```

    ## [1] 2 3 4 5 6

``` r
is.vector(my_vector_sapply)
```

    ## [1] TRUE

You see, we used **sapply** in exactly the same manner as we had used
**lapply**. However, the output is returned as a vector this time.

Similarly, we can define any other function and run it on a vector and
get the return in the form of a vector by using **sapply**. Here is
another example:

``` r
double_input <- function(number) {
  return(number*2)
}

my_vector_double <- sapply(my_vector, double_input)
my_vector_double
```

    ## [1]  2  4  6  8 10

Here we defined a function called *double\_input* that takes a number as
input and returns the product of the number with 2. Since we used
sapply, we were to able to retrieve a vector as the output from sapply.

### Functions that require more than one input

While lapply/sapply seems a great way to call a function on all elements
of a list/vector, it does seem that such functions can only process one
input which is the element from the vector. What if instead of
*add\_one*, we want to use a function that will take a vector and
another number as an input and then add this number to the function.
This can be achieved using the following:

``` r
add_number <- function(number, add_choice) {
  return(number + add_choice)
}

my_vector_incremened_1 <- sapply(my_vector, add_number, 1)
my_vector_incremened_1
```

    ## [1] 2 3 4 5 6

``` r
my_vector_incremened_2 <- sapply(my_vector, add_number, 2)
my_vector_incremened_2
```

    ## [1] 3 4 5 6 7

This brings us to the end of the first part of the tutorial dealing with
apply and sapply.
