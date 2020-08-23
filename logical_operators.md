Comparison and Logical operators
================
Virag Sharma

## Comparison operators

Comparison operator allow us to make different comparisons and test
different conditions. Let us look at some examples

``` r
x <- 10
# Ask if x is greater than 10
x > 10
```

    ## [1] FALSE

``` r
# Ask if x is less than 10
x < 10
```

    ## [1] FALSE

``` r
# Ask if x is equal to 100
x == 10
```

    ## [1] TRUE

Notice that to test if x is equal to 10, we need to make use of **two
equals to signs.**  
This is important to learn because a single equal to sign is the same as
assignment operator. Let us see this in action once

``` r
# assign a value of 10 to x
x <- 10
# and confirm if x is indeed equals to 10
x
```

    ## [1] 10

``` r
# Now assign a value of 0 to x
x = 0
x
```

    ## [1] 0

``` r
# And lastly, assign a value of 10 to x using a single equals to sign
x = 5
x
```

    ## [1] 5

As you can see, we use a **single equals to sign for an assignment
operation** i.e. assigning a value of 5 to x. This is in sharp contrast
to the use of **two equals to signs which tests a condition** i.e. if x
is equal to a certain value

``` r
# check if x is equal to 5
x == 5
```

    ## [1] TRUE

If you have learnt a bit of programming in some other language before,
then this concept should seem pretty familiar to you. All other
comparison operators are seeminly intuitive barring one.

``` r
# if x is greater than 5
x > 5
```

    ## [1] FALSE

``` r
# if x is less than 5
x < 5
```

    ## [1] FALSE

``` r
# if x is not equal to 5
x != 5
```

    ## [1] FALSE

The last test, checking if x is not equal to 5, makes use of the
exclamation sign **\!**.  
We will return to the exclamation sign as we discuss more of the logical
operators.

## Logical operators

Logical operators allow us to combine multiple comparison operators. We
will learn about the following logical operators:  
1\. AND &  
2\. OR |  
3\. NOT \!

Let us start with some examples:

#### AND Logical operator - &

The logical operator AND is used when we want to test for more than one
condition and to get a final TRUE value as the result of these
conditions, each one of these conditions need to individually return a
TRUE value

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < 20
```

    ## [1] TRUE

``` r
# now combine the two conditions
x == 10 & x < 20
```

    ## [1] TRUE

As you can see, we get a TRUE value at the end because the individual
conditions return a TRUE value. Let us look at a different example.

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < -20
```

    ## [1] FALSE

``` r
# now combine the two conditions
x == 10 & x < -20
```

    ## [1] FALSE

Expectedly, we get a FALSE value because one of the conditions (x \<
-20) return a FALSE value. Lastly and again expectedly, we will get a
FALSE value when all of the tested conditions will return a FALSE value

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < -20
```

    ## [1] FALSE

``` r
# now combine the two conditions
x == 11 & x < -20
```

    ## [1] FALSE

So to conclude, the AND logical operator allows you to combine several
conditions and the final result is TRUE only if all the conditions
individually return TRUE

#### OR Logical operator - |

The logical operator OR is used when we want to test for more than one
condition and to get a final TRUE value as the result of these
conditions, only one of these conditions need to individually return a
TRUE value.  
Here is an example

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < -20
```

    ## [1] FALSE

``` r
# now combine the two conditions
x == 10 | x < -20
```

    ## [1] TRUE

In contrast to the AND logical operator, we get a TRUE value as the
final result because at least one of the conditions we tested returned
TRUE. As expected, we will get a FALSE value as the output if none of
the conditions return a TRUE value

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < -20
```

    ## [1] FALSE

``` r
# now combine the two conditions
x == 11 | x < -20
```

    ## [1] FALSE

#### NOT Logical operator - \!

The logical operator NOT is different from the AND and the OR operator
because NOT is not really used to test for multiple conditions, though
in priciple it could be used for any number of conditions. However, in
essence, the logical operator NOT tests if a condition (or a combination
of values) return a non TRUE (or FALSE) value.  
Here is NOT in action

``` r
x <- 10
x == 10
```

    ## [1] TRUE

``` r
! x == 10
```

    ## [1] FALSE

As can be see, the first condition (x is equal to 10) returns a TRUE
value. However, if we append a NOT operator to the outcome of this
condition, we get a FALSE value.  
So you could also think of NOT as an operator than can invert a TRUE to
a FALSE value.  
The NOT operator could easily be used in combination with AND and OR
logical operators

Here is AND and NOT combined:

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < -20
```

    ## [1] FALSE

``` r
# now combine the two conditions and use NOT 
! x == 11 & x < -20
```

    ## [1] FALSE

Here is AND and OR combined:

``` r
x <- 10
# check if x is equal to 10
x == 10
```

    ## [1] TRUE

``` r
# check if x is less than 20
x < -20
```

    ## [1] FALSE

``` r
# now combine the two conditions and use NOT 
! x == 11 | x < -20
```

    ## [1] TRUE

This brings us to the end of our tutorial on comparison and logical
operators
