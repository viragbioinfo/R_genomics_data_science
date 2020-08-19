VECTORS
================
Virag Sharma

The most common data structure in R is the **‘vector’**.  
Vectors are simpy collection of elements of the **same** type. A vector
is most commonly created using the *c()* function

### Creating a vector

Here is some code illustrating how to create vectors and how to do some
basic operations with them

``` r
my_vector <- c(1, 2, 3, 4, 5)
```

This creates a vector from elements 1 to 5 To see how your vector looks
like, type my\_vector in your console

``` r
my_vector
```

    ## [1] 1 2 3 4 5

You could also create the same vector using the colon notation. This
produces a vector with continuous numbers from the start till the end

``` r
my_vector <- 1:5
my_vector
```

    ## [1] 1 2 3 4 5

To determine the length of the vector, you use the *length* function

``` r
length(my_vector)
```

    ## [1] 5

To really verify that the data structure you created is indeed a vector,
you could use the *is.vector* function

``` r
is.vector(my_vector)
```

    ## [1] TRUE

You see a TRUE value which confirms that your data strucure is a vector

Now that you have created a vector that contains 5 elements starting
from 1 till 5, we will see how to do some basic operations with a vector
in the following exercises

### Basic operations with a vector

``` r
my_vector + 2
```

    ## [1] 3 4 5 6 7

``` r
my_vector
```

    ## [1] 1 2 3 4 5

As you can see every element in the vector got incremented by 2 This is
the essence of the operations you do on a vector. The operation is
applied to every single element in the vector

``` r
my_vector - 2
```

    ## [1] -1  0  1  2  3

Every element gets decremented by 2

Multiply the vector by 2

``` r
my_vector * 2
```

    ## [1]  2  4  6  8 10

Divide the vector by 2

``` r
my_vector/2
```

    ## [1] 0.5 1.0 1.5 2.0 2.5

However, the original vector that we created remains unperturbed. To
verify this, just type my\_vector

``` r
my_vector
```

    ## [1] 1 2 3 4 5

To really change the values in the original vector, you will need to the
assignment operation

``` r
my_vector <- my_vector*2
```

Here you are assigning the vector ‘my\_vector’ to the new value of
my\_vector

``` r
my_vector
```

    ## [1]  2  4  6  8 10

Alternatively, you could also assign this value to a different vector.
But let us get the original my\_vector back

``` r
my_vector <- 1:5
my_vector_new <- my_vector*2
my_vector
```

    ## [1] 1 2 3 4 5

``` r
my_vector_new
```

    ## [1]  2  4  6  8 10

So far we have seen how to create vectors and how to do some operations
on these vectors.

### How do we retrieve particular element(s) of a vector?

To do this, we use the index of the elements of the vector An important
point to be noted is that **R uses 1 as the first indexing position**
and not 0 which is used by most of the programming languages

Okay, lets go about extracting elements from our vector

``` r
my_vector[1]
```

    ## [1] 1

Hmm, that’s fine I want the first 2 elements

``` r
my_vector[1:2]
```

    ## [1] 1 2

I want the first, second and the fourth element

``` r
my_vector[c(1,2,4)]
```

    ## [1] 1 2 4

I want the first, second, third, and the fifth element

``` r
my_vector[c(1,2,3,5)]
```

    ## [1] 1 2 3 5

Is there a different way, I do not want to type this much?

``` r
my_vector[c(1:3,5)]
```

    ## [1] 1 2 3 5

Is there a way to just exclude the fourth element?

``` r
my_vector[-4]
```

    ## [1] 1 2 3 5

Lastly, is there a way to exclude more than one element, say exclude the
second and the fourth element?

``` r
  my_vector[-c(2,4)]
```

    ## [1] 1 3 5

### Other operations and functions with vectors

You may need to create a vector of a finite length that is a simply a
collection of the same element. Suppose we need to create a vector that
simply contains the numeric value 1, five times

``` r
my_vector <- c(1, 1, 1, 1, 1)
my_vector
```

    ## [1] 1 1 1 1 1

However, what if you need the numeric value 1, a hundred times. Typing
this 100 times is not fun and definitely prone to errors. Here the
function rep comes to your rescue

``` r
my_vector <- rep(1, 100)
```

It takes two arguments, the first one (1 in the above example) is the
element you want to be repeated and the second argument (100 in the
above example) is the number of repetitions of the element. Let us check
what did the function rep
    do?

``` r
my_vector
```

    ##   [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
    ##  [38] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
    ##  [75] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

You may also need to create a vector where you want to start at a
specific point, end at a specific point and you want a specific interval
between two successive elements of this vector The function seq comes to
your rescue here

``` r
seq(1, 10)
```

    ##  [1]  1  2  3  4  5  6  7  8  9 10

Here you just specified the start and the end points. But we could
specify the step size as well:

``` r
seq(1, 10, by = 2)
```

    ## [1] 1 3 5 7 9

So essentially you have created a vector of odd numbers that lie between
1 to 10

``` r
seq(0, 10, by = 2)
```

    ## [1]  0  2  4  6  8 10

The above creates a list of even numbers that lie between 0 to 10 Since
0 is strictly speaking neither odd nor even, you will need to start at 2

``` r
seq(2, 10, by = 2)
```

    ## [1]  2  4  6  8 10

Lastly, vectors can also be **named** which means that you can
identify/extract elements from a vector either by their index or from
their names Here is how you do this

``` r
my_vector <- 1:5
my_names <- c('A', 'B', 'C', 'D', 'E')
names(my_vector) <- my_names
my_vector
```

    ## A B C D E 
    ## 1 2 3 4 5

Here you will see a vector which is distributed along two horizonal
lines, the first line indicates the names (A, B, C) while the second
line indicates the actual value of the elements of the vector. However,
this is a normal vector and you could do the operations you would do
with a vector

``` r
x1 = my_vector[1:2]
x1 * 2
```

    ## A B 
    ## 2 4

``` r
x = my_vector[1]
y = my_vector[2]
z = x + y
```

At some point you may want to get rid of the names of the vector
elements. For instance, in the above x + y example, you still have the
name “A” assigned to the single element of vector z. The function
*unname* does the job here

``` r
unname(z)
```

    ## [1] 3

### Subsetting a vector

Lastly, one of the most important operations you will need to do on a
datastructure in R (whether it is a vector, matrix or a dataframe) is to
subset your datastructure according to some condition. Imagine we have a
vector of logicals and we only want those that have TRUE value. This can
be done by passing the condition using the bracket notation to the
vector:

``` r
my_log_vector <- c(TRUE, FALSE, FALSE, TRUE, TRUE, TRUE, FALSE, TRUE, TRUE, TRUE, FALSE)
my_log_vector[my_log_vector == TRUE]
```

    ## [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE

To break this down, you can see the output of the condition first

``` r
my_log_vector[my_log_vector == TRUE]
```

    ## [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE

This is simply a vector of logicals telling you which indexes in your
vector meet your condition. Once you have this vector, passing this to
the original vector in the bracket notation only returns TRUE values

Another example where we have a vector of scores in the Bioinformatics
module for 10 students

``` r
bioinfo_scores <- c(90, 63, 73, 89, 74, 92, 86, 70, 83, 90)
# scores greater than 90
bioinfo_scores[bioinfo_scores > 90]
```

    ## [1] 92

``` r
# scores greater than 80
bioinfo_scores[bioinfo_scores > 80]
```

    ## [1] 90 89 92 86 83 90

``` r
# scores greater than 70
bioinfo_scores[bioinfo_scores > 70]
```

    ## [1] 90 73 89 74 92 86 83 90

``` r
# scores less than 70
bioinfo_scores[bioinfo_scores < 70]
```

    ## [1] 63

If you are interested in counting the number of students instead of just
looking at the scores, then you can pass the condition to the *length*
function \# scores greater than 90
length(bioinfo\_scores\[bioinfo\_scores \> 90\]) \# scores greater than
80 length(bioinfo\_scores\[bioinfo\_scores \> 80\]) \# scores greater
than 70 length(bioinfo\_scores\[bioinfo\_scores \> 70\]) \# scores less
than 70 length(bioinfo\_scores\[bioinfo\_scores \< 70\]) \`\`\`

This brings us to the end of our tutorial on vectors, we will discuss
matrices in the next tutorial
