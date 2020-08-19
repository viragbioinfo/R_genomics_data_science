DATAFRAMES: Part 3
================
Virag Sharma

### Subsetting dataframes

It happens very often that you have a data-frame but you acquired this
dataframe from an external source/collaborator and you may not want to
have all the variables in your dataframe i.e. you would like to drop
some columns.  
Secondly, you may want to apply some filters/thresholds to the different
variables in your data and see only those data points that pass the
filters. Lastly, you might want to re-order the columns in your
dataframe.  
The *subset* function comes to your rescue.

Let us start with the gulo\_df dataframe and do some subsetting
operations on
it

#### Operations involving entire columns

``` r
species <- c('mouse', 'rat', 'kangaroo_rat', 'guinea_pig', 'rabbit', 'human', 'chimp', 'horse', 'cat') ## Type_this
status <- c(T, T, T, F, T, F, F, T, T)
assembly_qual <- c(1, 1, 1, 1, 1, 1, 0, 1, 0)
gulo_df <- data.frame(species, status, assembly_qual)
```

Now imagine that we just want the species and the assembly\_qual columns
from this dataframe. We can subset the dataframe using the following:

``` r
subset(gulo_df, select = c('species', 'assembly_qual'))
```

    ##        species assembly_qual
    ## 1        mouse             1
    ## 2          rat             1
    ## 3 kangaroo_rat             1
    ## 4   guinea_pig             1
    ## 5       rabbit             1
    ## 6        human             1
    ## 7        chimp             0
    ## 8        horse             1
    ## 9          cat             0

Similarly, we can only subset the species and the status column from
this dataframe

``` r
subset(gulo_df, select = c('species', 'status'))
```

    ##        species status
    ## 1        mouse   TRUE
    ## 2          rat   TRUE
    ## 3 kangaroo_rat   TRUE
    ## 4   guinea_pig  FALSE
    ## 5       rabbit   TRUE
    ## 6        human  FALSE
    ## 7        chimp  FALSE
    ## 8        horse   TRUE
    ## 9          cat   TRUE

If we have a dataframe with 100 column names and we want to drop one or
two columns, a better option would be to specify the exclude columns
instead of listing all the columns you need. Below we specify that we
want to exclude the assembly\_qual column

``` r
subset(gulo_df, select = -c(assembly_qual))
```

    ##        species status
    ## 1        mouse   TRUE
    ## 2          rat   TRUE
    ## 3 kangaroo_rat   TRUE
    ## 4   guinea_pig  FALSE
    ## 5       rabbit   TRUE
    ## 6        human  FALSE
    ## 7        chimp  FALSE
    ## 8        horse   TRUE
    ## 9          cat   TRUE

Lastly, we can also re-order the columns in a dataframe. The order of
column names specified to the **“select”** argument in the subset call
determines the order of the columns of the dataframe. Below we do not
drop any column but simply reorder them.

``` r
subset(gulo_df, select = c(assembly_qual, status, species))
```

    ##   assembly_qual status      species
    ## 1             1   TRUE        mouse
    ## 2             1   TRUE          rat
    ## 3             1   TRUE kangaroo_rat
    ## 4             1  FALSE   guinea_pig
    ## 5             1   TRUE       rabbit
    ## 6             1  FALSE        human
    ## 7             0  FALSE        chimp
    ## 8             1   TRUE        horse
    ## 9             0   TRUE          cat

### Filtering dataframes to display only a subset of rows:

#### 1\. Making use of subset

If we want to find out only those species where the gene is intact
(status is set to TRUE), we use subset in the following form:

``` r
subset(gulo_df, subset = status == TRUE)
```

    ##        species status assembly_qual
    ## 1        mouse   TRUE             1
    ## 2          rat   TRUE             1
    ## 3 kangaroo_rat   TRUE             1
    ## 5       rabbit   TRUE             1
    ## 8        horse   TRUE             1
    ## 9          cat   TRUE             0

Similarly, we can find subset this data-frame to get only those species
where the gene is non-intact

``` r
subset(gulo_df, subset = status == FALSE)
```

    ##      species status assembly_qual
    ## 4 guinea_pig  FALSE             1
    ## 6      human  FALSE             1
    ## 7      chimp  FALSE             0

We can also set advanced filters. For instance, we want to see the
species where the Gulo gene is non-intact and the quality of genome
assembly is also good. Here use the “&” operator

``` r
subset(gulo_df, subset = status == FALSE & assembly_qual == 1)
```

    ##      species status assembly_qual
    ## 4 guinea_pig  FALSE             1
    ## 6      human  FALSE             1

Note that checking for equality warrants the use of ‘==’

#### 2\. Making use of the bracket and $ notation

We could also make use of a combination of the bracket and $ notation to
extract specific rows of a dataframe that meet our selection criteria
For instance, if we were to to look at only those species where the
status variable is set to TRUE, the following does the job for us:

``` r
gulo_df[gulo_df$status == T,]
```

    ##        species status assembly_qual
    ## 1        mouse   TRUE             1
    ## 2          rat   TRUE             1
    ## 3 kangaroo_rat   TRUE             1
    ## 5       rabbit   TRUE             1
    ## 8        horse   TRUE             1
    ## 9          cat   TRUE             0

To really understand what is happening under the hood, you could take a
look at the output of what is contained inside the brackets

``` r
gulo_df$status == T
```

    ## [1]  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE

So as you will see, you get back a logical vector which contains TRUE
for those row indices where your condition is met and FALSE for where it
is not.  
Hence the following call **gulo\_df\[gulo\_df$status == T,\]** is simply
specifying a list of row indexes (the ones which are FALSE are excluded)
and asking for all columns to be returned.

Like before, it is possible to add more thresholds, such as asking for
status == TRUE and assembly quality == 0

``` r
gulo_df[gulo_df$status == T & assembly_qual == 0,]
```

    ##   species status assembly_qual
    ## 9     cat   TRUE             0

### Ordering dataframes:

Now let us add another column to the dataframe where we indicate the
year in which the genome of the species listed in each row was
sequenced. Note that these are just made up numbers, for the time
being

``` r
gulo_df$sequencing_year <- c(2002,2004,2009,2006,2007,2001,2003,2008,2009)
gulo_df
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 4   guinea_pig  FALSE             1            2006
    ## 5       rabbit   TRUE             1            2007
    ## 6        human  FALSE             1            2001
    ## 7        chimp  FALSE             0            2003
    ## 8        horse   TRUE             1            2008
    ## 9          cat   TRUE             0            2009

We want to arrange the dataframe so that the sequencing year is arranged
in ascending order. We can use order to do this:

``` r
gulo_df[order(gulo_df['sequencing_year']),]
```

    ##        species status assembly_qual sequencing_year
    ## 6        human  FALSE             1            2001
    ## 1        mouse   TRUE             1            2002
    ## 7        chimp  FALSE             0            2003
    ## 2          rat   TRUE             1            2004
    ## 4   guinea_pig  FALSE             1            2006
    ## 5       rabbit   TRUE             1            2007
    ## 8        horse   TRUE             1            2008
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 9          cat   TRUE             0            2009

It is also possible to reverse this order by using the - sign

``` r
gulo_df[order(-gulo_df['sequencing_year']),]
```

    ##        species status assembly_qual sequencing_year
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 9          cat   TRUE             0            2009
    ## 8        horse   TRUE             1            2008
    ## 5       rabbit   TRUE             1            2007
    ## 4   guinea_pig  FALSE             1            2006
    ## 2          rat   TRUE             1            2004
    ## 7        chimp  FALSE             0            2003
    ## 1        mouse   TRUE             1            2002
    ## 6        human  FALSE             1            2001

To understand what is happening under the hood, we could simply see the
output of the order function

``` r
order(gulo_df['sequencing_year'])
```

    ## [1] 6 1 7 2 4 5 8 3 9

So essentially we get the indexes of the species when their sequencing
year is arranged in ascending order. After that, it is simply
specififying the list of row indexes to the dataframe.
