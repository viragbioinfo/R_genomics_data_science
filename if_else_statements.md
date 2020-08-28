IF statments
================
Virag Sharma

In this tutorial, we will discuss the *if* statement together with the
the *else* clause and lastly, nested *if-else* statements.  
Again, if you have some background in programming then you would have
heard of the if statement. Logically speaking, if statement is one of
the core concepts of programming and this remains true regardless of the
programming language you are talking about.

But what exactly, does an *if* statement does? Well, as the name
suggests, it tells you to test a condition i.e. what **IF** a condition
is true.

## The IF statement - solo

Let us look at a couple of examples:

``` r
x <- 5

number_small <- FALSE
if (x < 10) {
  number_small <- TRUE
}
number_small
```

    ## [1] TRUE

In terms of syntax, you may go back to the *for loop* syntax and see
some parallels here. However, the similarity between the *for loop* and
the *if* statement is only restricted to the syntax. Otherwise, both of
them do very different jobs.

The syntax for an *if* statement has a couple of elements:  
1\. The condition that we want to test. In the example we have seen
above, the condition is to test if the number x is smaller than 10 or
not. 2. Some action after the outcome of the conditional test is known.
Simply speaking, after we know that x is smaller than 10 or not, we
perform some operation. In the above example, if the number x is found
to be smaller than 10, then we set the value of a logical variable
called number\_small to TRUE.

Just to confirm that the logical variable *number\_small* gets a true
value only if the number (x) is smaller than 10, let us try with a
different value of x.

``` r
x <- 20

number_small <- FALSE
if (x < 10) {
  number_small <- TRUE
}
number_small
```

    ## [1] FALSE

Running the above code sets does not change the value of the logical
because the *if* condition is not met, and since it is not met, the code
following the *if* statement does not get executed.

## The IF statement - together with the ELSE clause

We have seen that when the *if* statement results a true value, then
some code gets executed. But sometimes we might want to execute some
other code when the *if* statement does not return a true value. This is
essentially the inverse of the *if* statement – do some action following
the failure of the *if* statement. This is achieved by using the *else*
clause together with the *if* clause. Here is a simple example
demonstrating the if-else combination in action:

``` r
x <- 20
number_small <- ''
if (x < 10) {
  number_small <- TRUE
} else {
  number_small <- FALSE  
}
number_small
```

    ## [1] FALSE

To begin with, we did not set the value of the logical *number\_small*
to either **TRUE** or **FALSE**. Then we simply used our *if* condition
as before. Is our number less than 10 or not?  
If the answer is yes, then we set the value of the logical to *TRUE* but
if our number is not less than 10, then this logical gets the *FALSE*
value.  
Note that this is different from using the *if* condition without the
*else* clause because in the absence of the *else* clause, the value of
the logical would remain equal to an empty object.  
Let’s try this:

``` r
x <- 20
number_small <- ''
if (x < 10) {
  number_small <- TRUE
}
number_small
```

    ## [1] ""

Notice that you get nothing in the output when you try to print the
logical *number\_small*

## The IF-ELSE-IF combo

Lastly, there might be a situation where you want to test multiple
conditions. Such situtations warrant the use of *if-else-if* nested
statements.  
Let us look at an example first to get a better understanding:

``` r
option <- 1
food_item <- ''

if (option == 1) {
  food_item <- 'ice-cream'  
} else if (option == 2) {
  food_item <- 'sushi'
} else if (option == 3) {
  food_item <- 'a cold beverage'
}
food_item
```

    ## [1] "ice-cream"

Here we have a variable called option that is currently set to 1. As can
be seen from the code, we have the first *if* condition that tests if
the value is set to 1. If yes, then the value *ice-cream* is assigned to
an empty object called food\_item.  
In the next statement, we ask that if the previous *if* statement did
not return a TRUE value, which is conceptually similar to the *else*
keyword, then we have another *if* condition which tests if the option
has a value equal to 2. If this condition is met, then the value *sushi*
is assigned to an empty object called food\_item. Similarly, we ask
again if the previous *if* statement did not return a TRUE value, i.e.
*else* followed by have another *if* condition which tests if the option
has a value equal to 3. If this condition is met, then the value *a cold
beverage* is assigned to an empty object called food\_item.

Let us change the value of the option variable to convince ourselves
that indeed this is how the if-else-if block works.

``` r
option <- 2
food_item <- ''

if (option == 1) {
  food_item <- 'ice-cream'  
} else if (option == 2) {
  food_item <- 'sushi'
} else if (option == 3) {
  food_item <- 'a cold beverage'
}
food_item
```

    ## [1] "sushi"

And once more by setting the value of *option* to 3

``` r
option <- 3
food_item <- ''

if (option == 1) {
  food_item <- 'ice-cream'  
} else if (option == 2) {
  food_item <- 'sushi'
} else if (option == 3) {
  food_item <- 'a cold beverage'
}
food_item
```

    ## [1] "a cold beverage"

Note that we may also end this *if-else-if* combination by a terminal
*else* statement. This else statement will contain the block of code
that should be executed in case none of the if statements return a
**TRUE** value

And once more by setting the value of *option* to 3

``` r
option <- 100
food_item <- ''

if (option == 1) {
  food_item <- 'ice-cream'  
} else if (option == 2) {
  food_item <- 'sushi'
} else if (option == 3) {
  food_item <- 'a cold beverage'
} else {
  food_item <- 'french-fries'
}
  
food_item
```

    ## [1] "french-fries"

Here we set the value of the option to 100, which is not 1, 2 or 3.  
Hence the code in the terminal block which sets the value of the
*food-item* to *french-fries* gets executed.
