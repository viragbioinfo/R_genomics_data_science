LISTS
================
Virag Sharma

So far we have discussed vectors, matrices and dataframes. We have seen
that they have their own strengths and weaknesses. Vectors can only
store one kind of datatypes, the same applies to matrices too but
dataframes can overcome these limitations. Interestingly, there is yet
another data strucure that can combine all these data structures. It is
called a list. A list is an ordered collection of objects and allows you
to group related or unrelated objects as a single object

``` r
my_vec <- c(1, 2, 3)

mat_c1 <- c(1, 2, 3)
mat_c2 <- c(10, 20, 30)
my_matrix <- cbind(mat_c1, mat_c2)

df_c1 <- c(100, 200, 300)
df_c2 <- c('A', 'B', 'C')
my_df <- data.frame(df_c1, df_c2)
```

``` r
## print individual objects
my_vec
```

    ## [1] 1 2 3

``` r
class(my_vec)
```

    ## [1] "numeric"

``` r
my_matrix
```

    ##      mat_c1 mat_c2
    ## [1,]      1     10
    ## [2,]      2     20
    ## [3,]      3     30

``` r
class(my_matrix)
```

    ## [1] "matrix"

``` r
my_df
```

    ##   df_c1 df_c2
    ## 1   100     A
    ## 2   200     B
    ## 3   300     C

``` r
class(my_df)
```

    ## [1] "data.frame"

**Now if I want to combine the three objects together, then the list
becomes my go to data structure**

``` r
my_list <- list(d1 = my_vec, d2 = my_matrix, d3 = my_df)
# print and check the contents of the list
my_list
```

    ## $d1
    ## [1] 1 2 3
    ## 
    ## $d2
    ##      mat_c1 mat_c2
    ## [1,]      1     10
    ## [2,]      2     20
    ## [3,]      3     30
    ## 
    ## $d3
    ##   df_c1 df_c2
    ## 1   100     A
    ## 2   200     B
    ## 3   300     C

We can access the individual elements of the list using the bracket
notation

``` r
# Accessing the vector
my_list[[1]]
```

    ## [1] 1 2 3

``` r
# Accessing the matrix
my_list[[2]]
```

    ##      mat_c1 mat_c2
    ## [1,]      1     10
    ## [2,]      2     20
    ## [3,]      3     30

``` r
# Accessing the dataframe
my_list[[3]]
```

    ##   df_c1 df_c2
    ## 1   100     A
    ## 2   200     B
    ## 3   300     C

We can also verify if we get back the datatypes we expect by
**decomposing** this list

``` r
# Accessing the vector
is.vector(my_list[[1]])
```

    ## [1] TRUE

``` r
# Accessing the matrix
is.matrix(my_list[[2]])
```

    ## [1] TRUE

``` r
# Accessing the dataframe
is.data.frame(my_list[[3]])
```

    ## [1] TRUE

Lastly, we could also use the **$ notation** for the same purpose.

``` r
# Accessing the vector
is.vector(my_list$d1)
```

    ## [1] TRUE

``` r
# Accessing the matrix
is.matrix(my_list$d2)
```

    ## [1] TRUE

``` r
# Accessing the dataframe
is.data.frame(my_list$d3)
```

    ## [1] TRUE

This is all you need to know about the lists, for the time being. We
will discuss more specific use cases of lists in the following tutorials
