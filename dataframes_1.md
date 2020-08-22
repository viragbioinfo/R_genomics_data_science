DATAFRAMES: Part 1
================
Virag Sharma

Dataframes are perhaps the most commonly used data structures that you
will come across if you were to do some sophisticated analysis in R. A
dataframe is very similar to a matrix but it is more general than a
matrix and can store data of different types.

Data frames can be constructed using the *data.frame* function (Note
that *matrix* is for matrix construction, *data.frame* is for dataframe
construction). To begin with, let us use an example to see the
distinction between a matrix and a data-frame

``` r
c1 <- c(1,2,3,4)
c2 <- c('A', 'B', 'C', 'D')
class(c1)
```

    ## [1] "numeric"

``` r
class(c2)
```

    ## [1] "character"

As we can see, the vector c1 is a numeric vector while c2 is a character
vector

Here is the dataframe using these two vectors

``` r
my_first_df <- data.frame(c1, c2)
my_first_df
```

    ##   c1 c2
    ## 1  1  A
    ## 2  2  B
    ## 3  3  C
    ## 4  4  D

We have successfully created our first data-frame here.  
Let us now try creating a matrix using the same vectors.

``` r
my_test_matrix <- matrix(c(c1, c2), ncol = 2)
my_test_matrix
```

    ##      [,1] [,2]
    ## [1,] "1"  "A" 
    ## [2,] "2"  "B" 
    ## [3,] "3"  "C" 
    ## [4,] "4"  "D"

As you can see, the **numeric nature of the elements** in the first
column are **not preserved** and they are **changed to character**. This
is what separates a data frame from a matrix and makes it a very popular
data structure.  
**It can combine and hold different data-types together which is not
possible with a matrix.**

To give distinct names to the columns (also called as column headers)
when creating a data-frame, one could do the following

``` r
my_first_df <- data.frame(col1 = c1, col2 = c2)
```

Note that this data-frame is different from the first one we had created
because the column headers there were c1 and c2.

Another important aspect of a dataframe is the row names or the row
identifiers. In this case, they were automatically generated and are
integers starting from 1 until 4. But the *rownames* function we used to
assign identifiers to the rows in matrices could also be used to assign
row identifiers to a data-frame

``` r
rownames(my_first_df) <- c('r1', 'r2', 'r3', 'r4')
my_first_df
```

    ##    col1 col2
    ## r1    1    A
    ## r2    2    B
    ## r3    3    C
    ## r4    4    D

Similarly, you could also use *colnames* to assign names to columns or
over-write existing column names of a data-frame

``` r
colnames(my_first_df) <- c('column1', 'column2')
my_first_df
```

    ##    column1 column2
    ## r1       1       A
    ## r2       2       B
    ## r3       3       C
    ## r4       4       D

Again, similar to matrices, you could use the same functions to get the
dimensions of the matrix or get the number of rows or columns.

``` r
dim(my_first_df)
```

    ## [1] 4 2

``` r
nrow(my_first_df)
```

    ## [1] 4

``` r
ncol(my_first_df)
```

    ## [1] 2

Before we go further, let us flip the column names back to col1 and col2

``` r
colnames(my_first_df) <- c('col1', 'col2')
my_first_df
```

    ##    col1 col2
    ## r1    1    A
    ## r2    2    B
    ## r3    3    C
    ## r4    4    D

## Extacting rows or columns from a dataframe

There are several ways to extract the elements of a data frame. You can
extract specific columns using column numbers or column names, and
similarly, specific rows can be extracted using row numbers or row
identifier.

However, to understand the underlying logic behind this, you have to
understand that every element in a dataframe can be considered as a
point in an 2 dimensional plane. To identify this point, you need to
specify the x coordinate and the y coordinate. Quite similarly, to
extract an element from a dataframe, you need to specify the coordinate
along the row and then the coordinate along the column.

More specifically, if I say my\_first\_df\[1,2\] the first number (1)
indicates the position of the element along the the row-axis and the the
second number (2) indicates the position of the element along the
column-axis.

#### Extracting different columns

``` r
my_first_df[, 'col1']
```

    ## [1] 1 2 3 4

``` r
my_first_df[, 'col2']
```

    ## [1] A B C D
    ## Levels: A B C D

In this case, we do not specify any number along the row-axis. So this
essentially means that we are asking for all the rows but we have
specified the column axis. In this particular case, we specified the
column by its name in the data-frame. Similarly, we specified the second
column by its name in the second call.

``` r
my_first_df[, 1]
```

    ## [1] 1 2 3 4

``` r
my_first_df[, 2]
```

    ## [1] A B C D
    ## Levels: A B C D

There are two more ways to extract entire columns from a dataframe and
they make use of the column names. The first one makes use of the
**dollar notation i.e $ **

Here we append the column name to the dataframe but separate the two by
a **$** sign

``` r
my_first_df$col1
```

    ## [1] 1 2 3 4

The second one makes use of the double bracket notation. So we pass the
column name to the dataframe using double brackes

``` r
my_first_df[['col1']]
```

    ## [1] 1 2 3 4

Note that we discussed 4 different ways of extracting entire columns
from a dataframe and returning vectors. But 3 out of these 4 ways makes
use of the column names. Specifying columns by name is indeed useful
when we have a bigger dataframe that has several columns and you simply
cannot count the position of the column that is of interest to you.

#### Extracting different rows

Making use of the row name

``` r
my_first_df['r1', ]
```

    ##    col1 col2
    ## r1    1    A

Making use of the row index/position

``` r
my_first_df[1, ]
```

    ##    col1 col2
    ## r1    1    A

As you can see, we achieve the same results whether we use ‘r1’ i.e. the
name of the row or 1 which is the position of the row. Again using row
name is advantageous when you are dealing with a bigger dataframe that
has several rownames and you simply cannot count to get the position of
your row of interest.

#### Extracting individual elements from a dataframe

Now that we know how to identify specific rows and columns from a
dataframe, extracting a specific element is simply combining the two
together.

``` r
my_first_df['r1', 'col1']
```

    ## [1] 1

``` r
my_first_df['r2', 'col1'] 
```

    ## [1] 2

``` r
my_first_df['r3', 'col2']
```

    ## [1] C
    ## Levels: A B C D

#### Distinction between extracting rows and extracting columns from a dataframe

We have seen 4 different ways of extracting entire columns from a
dataframe and two different ways of extracting entire rows from a
dataframe. Let us revisit this and see what is the type of datastructure
that we retrieve from these operations.

``` r
my_first_df[, 1]
```

    ## [1] 1 2 3 4

``` r
my_first_df[, 'col1']
```

    ## [1] 1 2 3 4

``` r
my_first_df$col1
```

    ## [1] 1 2 3 4

``` r
my_first_df[['col1']]
```

    ## [1] 1 2 3 4

As you would see, we get a vector from all these operations. This could
also be confirmed by making use of the *is.vector* function.

``` r
is.vector(my_first_df[, 1])
```

    ## [1] TRUE

``` r
is.vector(my_first_df[, 'col1'])
```

    ## [1] TRUE

``` r
is.vector(my_first_df$col1)
```

    ## [1] TRUE

``` r
is.vector(my_first_df[['col1']])
```

    ## [1] TRUE

However, when we extract specific rows, we get a dataframe back

``` r
my_first_df['r1',]
```

    ##    col1 col2
    ## r1    1    A

``` r
is.data.frame(my_first_df['r1',])
```

    ## [1] TRUE

If you really want to extract a column and get a dataframe back, then
this can be achieved by making use of the single bracket notation

``` r
my_first_df['col1']
```

    ##    col1
    ## r1    1
    ## r2    2
    ## r3    3
    ## r4    4

``` r
is.data.frame(my_first_df['col1'])
```

    ## [1] TRUE

Now that we have learnt how to use the indexes or row/column names to
extract specific elements from a data-frame, we could re-visit the
matrices section to see if the same principles work with matrices as
well.
