lapply and sapply: Part 2
================
Virag Sharma

In this short tutorial, we are going to learn how to create anonymous
functions. If you have some programming experience with Python, then
this should remind you of lambda expressions in Python.

In the last tutorial, we have seen how to make use of lapply and sapply
to apply a function over every element of a vector. While this is
efficient, it also requires that we need to write the code for a
function. Again, this is not a problem but there are more elegant ways
of writing code in R and writing anonymous functions in one of them.

Anonymous functions allow you to create an un-named function (hence the
name **anonymous**) on the fly. This also means that you will have to
create this function again if you need the same functionality again. Let
us look at how to anonymise the add\_one function that we have seen
before:

``` r
my_vector <- 1:5
my_vector_updated <- sapply(my_vector, function(number) {number + 1})
my_vector_updated
```

    ## [1] 2 3 4 5 6

So while the output is exactly identical to what we achieved in the last
tutorial, notice that we do not have defined the *add\_one* function
here. Instead, we have created a function on the fly. Let us also
compare how the two differ: a function with a name versus an anonymous
function in terms of code by looking at the code for the *add\_one*
function:

``` r
add_one <- function(number) {
  return(number + 1)
}
## one-liner for anonymous function that does the same thing:
## function(number) {number + 1}
```

Note that the difference lies in the following:  
1\. There is no-name, hence anonymous function.  
2\. No return statment either, whatever is returned is enclosed in a
pair of curly braces.  
3\. Anonymous functions are one-liners unlike a named function which in
this case spans at least three lines.

Similarly, we can anonymize the *double\_input* function that we saw in
the last tutorial.

``` r
my_vector_doubled <- sapply(my_vector, function(number) { number*2 } )
my_vector_doubled
```

    ## [1]  2  4  6  8 10

Note that using the same style as before, we could anonymize the
*double\_input* function, implying that it does not have to be defined
before and could simply be put in one line.

### Anonymous functions that require more than one input

Anonymous functions are perfect when using with lapply/sapply because
they provide a quick means of writing a small function and not worrying
about naming them, placing them at the right place in the code.  
However, from what we have seen before, it does not seem possible that
such anonymous functions could take more than one input. What if instead
of *add\_one*, we want to use an anonymous function that will take a
vector and another number as an input and then add this number to the
function. This can be achieved using the following:

``` r
add_number <- function(number, add_choice) {
  return(number + add_choice)
}

my_vector_updated <- sapply(my_vector, add_number, 2)
my_vector_updated
```

    ## [1] 3 4 5 6 7
