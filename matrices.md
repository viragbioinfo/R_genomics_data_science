MATRICES
================
Virag Sharma

A matrix is a collection of rows and columns. Simply put, a matrix is a
collection of vectors. If you have only one vector, then you could
generate a matrix that has either one row or one column. But with a
collection of vectors, you could generate a nXm matrix where n is the
number of rows and m is the number of columns Keep in mind that a matrix
can only contain data of one kind. More on this when we get to data
frames.

## Creating a matrix

A matrix can be created by combining rows or columns using the *rbind*
or the *cbind* function, respectively

``` r
r1 <- 1:5
r2 <- seq(10, 50, by = 10)
mat_row = rbind(r1, r2)
```

This creates a matrix by simply putting the two rows on the top of each
other

``` r
mat_row
```

    ##    [,1] [,2] [,3] [,4] [,5]
    ## r1    1    2    3    4    5
    ## r2   10   20   30   40   50

Let us check the **dimensions** of the matrix. We use the *dim* function
to do that

``` r
dim(mat_row)
```

    ## [1] 2 5

Expectedly, it tells us that we have a matrix with 2 rows (which we used
to generate the matrix) and 5 columns (remember each vector r1 and r2
had 5 elements each) We could also do the same using the *nrow* or
*ncol* function individually

``` r
ncol(mat_row)
```

    ## [1] 5

``` r
nrow(mat_row)
```

    ## [1] 2

Let us now use *cbind* to create a matrix

``` r
c1 <- 1:5
c2 <- seq(10, 50, by = 10)
mat_col = cbind(c1, c2)
```

This creates a matrix by simply placing the two columns next to each
other

``` r
mat_col
```

    ##      c1 c2
    ## [1,]  1 10
    ## [2,]  2 20
    ## [3,]  3 30
    ## [4,]  4 40
    ## [5,]  5 50

``` r
dim(mat_col)
```

    ## [1] 5 2

Expectedly, it tells us that we have a matrix has 5 rows and 2 columns
(because we placed two vector next to each other and each vector has 5
elements)

A more direct (but less useful) way of creating a matrix is by listing
all the elements of a matrix and then specifying the number of rows or
columns you want. This is done by making use of the *matrix* function

``` r
my_matrix <- matrix(c(1,2,3,4,5,6), nrow = 2)
my_matrix
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    3    5
    ## [2,]    2    4    6

Note that the elements are distributed *column-wise*. The first two
elements (1,2) go to the first column, the next two (3,4) go the second
column while the last two elements (5,6) go to the last column

Let us specify the number of columns for the same set of elements

``` r
my_matrix <- matrix(c(1,2,3,4,5,6), ncol = 2)
my_matrix
```

    ##      [,1] [,2]
    ## [1,]    1    4
    ## [2,]    2    5
    ## [3,]    3    6

Like the previous example, the first three elements go to the first
column while the next three elements go to the second column. To
distribute the elements **row-wise**, you need to make use of the
**‘byrow’** argument from the matrix function

``` r
my_matrix <- matrix(c(1,2,3,4,5,6), ncol = 2, byrow = TRUE)
my_matrix
```

    ##      [,1] [,2]
    ## [1,]    1    2
    ## [2,]    3    4
    ## [3,]    5    6

Here we see that the first two elements are distributed along the first
row, the next two along the second row and lastly, the last elements are
distributed along the last row of the matrix.

### Assigning names to rows and columns:

The matrix that we created above has only 2 columns and 3 rows. Imagine
a matrix with 1,000 rows and 500 columns. Clearly it will be hard to
refer to first column, second column or first row, second row and so on.
However, it would be useful if we could have row names and column names
that can be used to refer to the different rows or columns of the
matrix. The functions *rownames* and *colnames* come to our rescue

Lets create a 3 by 2 matrix

``` r
my_matrix <- matrix(c(1,2,3,4,5,6), ncol = 2, byrow = TRUE) ## Type_this
my_matrix
```

    ##      [,1] [,2]
    ## [1,]    1    2
    ## [2,]    3    4
    ## [3,]    5    6

As you can see in the above matrix none of the rows or columns are
named. To name the rows, we use the *rownames* function:

``` r
rownames(my_matrix) <- c('r1', 'r2', 'r3') ## Type_this
```

To name the columns, we use the *colnames* function:

``` r
colnames(my_matrix) <- c('c1', 'c2') ## Type_this
```

We can now check if the matrix has names for both, rows and columns

``` r
my_matrix
```

    ##    c1 c2
    ## r1  1  2
    ## r2  3  4
    ## r3  5  6

As we can see the 3 rows have names (r1, r2 and r3) and the columns have
names (c1 and c2)

### Adding rows or columns to a matrix

Lastly, we will quickly have a look at how to add rows/columns to an
already existing matrix. This is simple because we have already seen the
functions *cbind* and *rbind* in action

Let us add another column to the matrix having values 7,8 and 9

``` r
cbind(my_matrix, c3 = c(7,8,9))
```

    ##    c1 c2 c3
    ## r1  1  2  7
    ## r2  3  4  8
    ## r3  5  6  9

Instead of adding another column, let us add another row to the matrix
having values 7 and 8

``` r
rbind(my_matrix, r4 = c(7,8))
```

    ##    c1 c2
    ## r1  1  2
    ## r2  3  4
    ## r3  5  6
    ## r4  7  8

Note that in both the cases, we added a column (c3) or a row (r4) that
already had names. Try doing the following:

``` r
cbind(my_matrix, c(7,8,9))
```

    ##    c1 c2  
    ## r1  1  2 7
    ## r2  3  4 8
    ## r3  5  6 9

``` r
rbind(my_matrix, c(7,8))
```

    ##    c1 c2
    ## r1  1  2
    ## r2  3  4
    ## r3  5  6
    ##     7  8

and compare the difference in outputs from the previous cbind/rbind
calls

### Arithmetic operations with matrices

These are very similar to the arithmetic operations with vectors that we
have seen before Essentially, you do the same arithmetic operation with
every element of the matrix

For example, let us create a 2 by 2 matrix

``` r
my_matrix <- matrix(c(1,2,3,4), ncol = 2, byrow = TRUE)
my_matrix
```

    ##      [,1] [,2]
    ## [1,]    1    2
    ## [2,]    3    4

Now let us do some simple arithmetic operations with the 2 by 2 matrix
we have created above

#### Addition

``` r
my_matrix + 2
```

    ##      [,1] [,2]
    ## [1,]    3    4
    ## [2,]    5    6

#### Multiplication

``` r
my_matrix * 2
```

    ##      [,1] [,2]
    ## [1,]    2    4
    ## [2,]    6    8

#### Subtraction

``` r
my_matrix - 2
```

    ##      [,1] [,2]
    ## [1,]   -1    0
    ## [2,]    1    2

#### Divison

``` r
my_matrix / 2
```

    ##      [,1] [,2]
    ## [1,]  0.5    1
    ## [2,]  1.5    2

#### Exponentiation

``` r
my_matrix ^ 2
```

    ##      [,1] [,2]
    ## [1,]    1    4
    ## [2,]    9   16

This brings us to the end of the matrices tutorial. I have purposefully
not discussed the indexing/selection of elements from matrix. We will
cover this aspect of matrices together with dataframes because matrices
and dataframes make use of the same principles/logic for indexing.
