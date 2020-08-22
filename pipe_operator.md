The pipe operator
================
Virag Sharma

As you will work more with the dataframes and use the dplyr package, and
especially if you read R-code written by others, you will repeatdely
bump into the pipe operator. The pipe operator looks like the following
**%\>%**.

Essentially it allows you to chain different operations and write a
single statement consisting of multiple operations instead of assigning
results of each operation to an individual dataframe and then working
with this dataframe for the subsequent operation.  
Let us illustrate this with an example by using our gulo\_df
dataframe.

``` r
species <- c('mouse', 'rat', 'kangaroo_rat', 'guinea_pig', 'rabbit', 'human', 'chimp', 'horse', 'cat') ## Type_this
status <- c(T, T, T, F, T, F, F, T, T) ## Type_this
assembly_qual <- c(1, 1, 1, 1, 1, 1, 0, 1, 0) ## Type_this
gulo_df <- data.frame(species, status, assembly_qual) ## Type_this
sequencing_year <- c(2002,2004,2009,2006,2007,2001,2003,2008,2009)
gulo_df <- data.frame(species, status, assembly_qual, sequencing_year)
```

Suppose we want to filter for those species where the gene is intact and
then arrange those species in order of the year their genome was
sequenced. We could do it using two ways:

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
# Using nesting
arrange(filter(gulo_df, status == T), sequencing_year)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3       rabbit   TRUE             1            2007
    ## 4        horse   TRUE             1            2008
    ## 5 kangaroo_rat   TRUE             1            2009
    ## 6          cat   TRUE             0            2009

This comes with the hassle that you have to read the code inside out.
First you have to look at the inner-most function which is filter, and
then go outwards to the arrange function. Of course, it works but is not
so elegant.

The other way to do this would be to assign results to individual
dataframes

``` r
# Using multiple dataframes
df1 <- filter(gulo_df, status == T)
arrange(df1, sequencing_year)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3       rabbit   TRUE             1            2007
    ## 4        horse   TRUE             1            2008
    ## 5 kangaroo_rat   TRUE             1            2009
    ## 6          cat   TRUE             0            2009

Here you have created a dataframe df1, that you can then use as an input
for the *arrange* function.  
The **%\>%** allows you to chain these operations.  
In principle, this could be considered as the R-equivalent of Unix’s
pipe (written as **|**).  
Here is **%\>%** in action

``` r
# Using pipe operator
gulo_df %>% filter(status == T) %>% arrange(sequencing_year)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3       rabbit   TRUE             1            2007
    ## 4        horse   TRUE             1            2008
    ## 5 kangaroo_rat   TRUE             1            2009
    ## 6          cat   TRUE             0            2009

So as you can see, this simplifies the code tremendously. You start with
your dataframe and then you start to pipe it to different functions
(*filter* and *arrange* in the above example). Notice that you also do
not need to pass the dataframe as the first argument to filter or
arrange function.

The pipe operator is going to be a good friend of yours if you have a
dataframe that needs to be processed using a combination of different
functions.
