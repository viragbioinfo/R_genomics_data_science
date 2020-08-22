The dplyr package
================
Virag Sharma

In the tutorial on dataframes, we saw how to use the subset function to
impose conditions on a dataframe and filter for only those rows/columns
that fulfill our conditions i.e. pass the filters. I have to admit that
I do not find the syntax extremely friendly and elegant and I guess I am
not alone. To overcome these limitations, the R package dplyr was
developed.

Note that dplyr is an external package. So you will need to install
dplyr on your machine. It is possible that you already have dplyr on
your machine and in that case, you can skip the installation.

``` r
# install.packages(dplyr)
```

Before we start to make use of the dplyr package, let us create the Gulo
gene dataframe again.

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
species <- c('mouse', 'rat', 'kangaroo_rat', 'guinea_pig', 'rabbit', 'human', 'chimp', 'horse', 'cat') ## Type_this
status <- c(T, T, T, F, T, F, F, T, T) ## Type_this
assembly_qual <- c(1, 1, 1, 1, 1, 1, 0, 1, 0) ## Type_this
gulo_df <- data.frame(species, status, assembly_qual) ## Type_this
sequencing_year <- c(2002,2004,2009,2006,2007,2001,2003,2008,2009)
gulo_df <- data.frame(species, status, assembly_qual, sequencing_year)

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

``` r
dim(gulo_df)
```

    ## [1] 9 4

We would also need to load the dplyr library

``` r
library(dplyr)
```

Now let us make use of some of the functions from the dplyr package and
see what all we can do those functions.

#### filter()

The function, as the name tells you, allows to filter a dataframe for
certain
conditions.

``` r
## filter and get only those species where the gene is intact i.e. status is equal to T
filter(gulo_df, status == T)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 4       rabbit   TRUE             1            2007
    ## 5        horse   TRUE             1            2008
    ## 6          cat   TRUE             0            2009

So essentially the filter function takes two arguments. The name of the
dataframe and the condition. You could easily add more conditions to
your filter.

``` r
filter(gulo_df, status == T, assembly_qual > 0)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 4       rabbit   TRUE             1            2007
    ## 5        horse   TRUE             1            2008

Lets add even more conditions

``` r
filter(gulo_df, status == T, assembly_qual > 0, sequencing_year > 2004)
```

    ##        species status assembly_qual sequencing_year
    ## 1 kangaroo_rat   TRUE             1            2009
    ## 2       rabbit   TRUE             1            2007
    ## 3        horse   TRUE             1            2008

Note that in the above code, you are asking all the conditions to be met
i.e. you are making use of the boolean AND. To make use of OR instead
where the function returns a row if one of the several conditions is
met, you need to do the
following:

``` r
filter(gulo_df, status == T | assembly_qual > 0 | sequencing_year > 2004)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 4   guinea_pig  FALSE             1            2006
    ## 5       rabbit   TRUE             1            2007
    ## 6        human  FALSE             1            2001
    ## 7        horse   TRUE             1            2008
    ## 8          cat   TRUE             0            2009

To confirm that simply putting commas between conditions is equivalent
to the boolean AND, let us try one more thing.

``` r
## Using AND between the conditions
filter(gulo_df, status == T & assembly_qual > 0 & sequencing_year > 2004)
```

    ##        species status assembly_qual sequencing_year
    ## 1 kangaroo_rat   TRUE             1            2009
    ## 2       rabbit   TRUE             1            2007
    ## 3        horse   TRUE             1            2008

``` r
## Using commas between the conditions
filter(gulo_df, status == T, assembly_qual > 0, sequencing_year > 2004)
```

    ##        species status assembly_qual sequencing_year
    ## 1 kangaroo_rat   TRUE             1            2009
    ## 2       rabbit   TRUE             1            2007
    ## 3        horse   TRUE             1            2008

Lastly, to contrast the other ways of subsetting dataframes that we have
learnt before, let us have a look again:

``` r
## Using subset
subset(gulo_df, subset = status == T & assembly_qual > 0 & sequencing_year > 2004)
```

    ##        species status assembly_qual sequencing_year
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 5       rabbit   TRUE             1            2007
    ## 8        horse   TRUE             1            2008

``` r
## Using bracket_notation
gulo_df[gulo_df$status == T & gulo_df$assembly_qual > 0 & gulo_df$sequencing_year > 2004,]
```

    ##        species status assembly_qual sequencing_year
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 5       rabbit   TRUE             1            2007
    ## 8        horse   TRUE             1            2008

While all the three methods produce identical results, the one using the
filter function seems the easiest to comprehend. Having said that, there
seems to be one obvious drawback of using the filter function. What is
that?

#### slice()

The slice function allows us to select rows by using their indices.

``` r
slice(gulo_df, 1:5)
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 4   guinea_pig  FALSE             1            2006
    ## 5       rabbit   TRUE             1            2007

You could also supply a vector instead of the row elements you are
interesed in.

``` r
slice(gulo_df, c(1:5, 7:8))
```

    ##        species status assembly_qual sequencing_year
    ## 1        mouse   TRUE             1            2002
    ## 2          rat   TRUE             1            2004
    ## 3 kangaroo_rat   TRUE             1            2009
    ## 4   guinea_pig  FALSE             1            2006
    ## 5       rabbit   TRUE             1            2007
    ## 6        chimp  FALSE             0            2003
    ## 7        horse   TRUE             1            2008

### arrange()

As the name suggests, the *arrange* function can be used to reorder or
rearrange the rows of a dataframe. The syntax is straight forward – the
name of the dataframe followed by the names of the columns that you want
to reorder.

``` r
arrange(gulo_df, assembly_qual, sequencing_year)
```

    ##        species status assembly_qual sequencing_year
    ## 1        chimp  FALSE             0            2003
    ## 2          cat   TRUE             0            2009
    ## 3        human  FALSE             1            2001
    ## 4        mouse   TRUE             1            2002
    ## 5          rat   TRUE             1            2004
    ## 6   guinea_pig  FALSE             1            2006
    ## 7       rabbit   TRUE             1            2007
    ## 8        horse   TRUE             1            2008
    ## 9 kangaroo_rat   TRUE             1            2009

As we can see that since we ordered by assembly\_qual, we see the
species with 0 as the assembly\_quality value at the top. The default is
ascending order but you could also use the *desc* function to arrange in
descending order

``` r
## In ascending order
arrange(gulo_df, sequencing_year)
```

    ##        species status assembly_qual sequencing_year
    ## 1        human  FALSE             1            2001
    ## 2        mouse   TRUE             1            2002
    ## 3        chimp  FALSE             0            2003
    ## 4          rat   TRUE             1            2004
    ## 5   guinea_pig  FALSE             1            2006
    ## 6       rabbit   TRUE             1            2007
    ## 7        horse   TRUE             1            2008
    ## 8 kangaroo_rat   TRUE             1            2009
    ## 9          cat   TRUE             0            2009

``` r
## In descending order
arrange(gulo_df, desc(sequencing_year))
```

    ##        species status assembly_qual sequencing_year
    ## 1 kangaroo_rat   TRUE             1            2009
    ## 2          cat   TRUE             0            2009
    ## 3        horse   TRUE             1            2008
    ## 4       rabbit   TRUE             1            2007
    ## 5   guinea_pig  FALSE             1            2006
    ## 6          rat   TRUE             1            2004
    ## 7        chimp  FALSE             0            2003
    ## 8        mouse   TRUE             1            2002
    ## 9        human  FALSE             1            2001

### select()

Select allows you to only look at the columns of interest and discard
the ones that you do not want to see.

``` r
select(gulo_df, species)
```

    ##        species
    ## 1        mouse
    ## 2          rat
    ## 3 kangaroo_rat
    ## 4   guinea_pig
    ## 5       rabbit
    ## 6        human
    ## 7        chimp
    ## 8        horse
    ## 9          cat

Here you see only the species column of your dataframe.

At the same time, select also allows you to re-arrange the positions of
columns in your dataframe if needed.

``` r
select(gulo_df, sequencing_year, species)
```

    ##   sequencing_year      species
    ## 1            2002        mouse
    ## 2            2004          rat
    ## 3            2009 kangaroo_rat
    ## 4            2006   guinea_pig
    ## 5            2007       rabbit
    ## 6            2001        human
    ## 7            2003        chimp
    ## 8            2008        horse
    ## 9            2009          cat

Here you see that sequencing\_year becomes the first column in your
dataframe, followed by the species column which was originally the first
column in your dataframe.

### rename()

Rename lets you rename the columns of your dataframe

``` r
rename(gulo_df, seq_year = sequencing_year)
```

    ##        species status assembly_qual seq_year
    ## 1        mouse   TRUE             1     2002
    ## 2          rat   TRUE             1     2004
    ## 3 kangaroo_rat   TRUE             1     2009
    ## 4   guinea_pig  FALSE             1     2006
    ## 5       rabbit   TRUE             1     2007
    ## 6        human  FALSE             1     2001
    ## 7        chimp  FALSE             0     2003
    ## 8        horse   TRUE             1     2008
    ## 9          cat   TRUE             0     2009

Again the syntax is fairly straight-forward. You pass the dataframe
followed by the new column name, a single equals to sign i.e. ‘=’ and
the existing column name This can also be extended to other column names

``` r
rename(gulo_df, seq_year = sequencing_year, ass_qual = assembly_qual)
```

    ##        species status ass_qual seq_year
    ## 1        mouse   TRUE        1     2002
    ## 2          rat   TRUE        1     2004
    ## 3 kangaroo_rat   TRUE        1     2009
    ## 4   guinea_pig  FALSE        1     2006
    ## 5       rabbit   TRUE        1     2007
    ## 6        human  FALSE        1     2001
    ## 7        chimp  FALSE        0     2003
    ## 8        horse   TRUE        1     2008
    ## 9          cat   TRUE        0     2009

### mutate()

A very important functionality that dplyr offers is to create new
columns that contain information derived from the existing columns. To
illustrate this, let us add another column to our existing
dataframe

``` r
gulo_df_new <- data.frame(gulo_df, gulo_loss_year = c(2003, 2006, 2011, 2007, 2010, 2002, 2008, 2010, 2011))
```

Now our dataframe has a new column which tells you when the status of
the Gulo gene was ascertained (whether the gene is intact or not) in the
corresponding species (again, these numbers are made up).  
As can be expected, the numbers in this column are always greater than
the numbers in the column that correspond to the year in which the
species’ genome was sequenced. This makes sense because the status of
the gene i.e. Gulo in a species could only be ascertained after the
genome sequence of the species is available.  
Imagine that we want to have a column which tells us the time gap
between the sequencing of a species’ genome and the year when the status
of Gulo was ascertained. *mutate* precisely does that because it will
obtain this information from the existing columns and then put this new
information in a new
    column

``` r
mutate(gulo_df_new, time_gap = gulo_loss_year - sequencing_year)
```

    ##        species status assembly_qual sequencing_year gulo_loss_year time_gap
    ## 1        mouse   TRUE             1            2002           2003        1
    ## 2          rat   TRUE             1            2004           2006        2
    ## 3 kangaroo_rat   TRUE             1            2009           2011        2
    ## 4   guinea_pig  FALSE             1            2006           2007        1
    ## 5       rabbit   TRUE             1            2007           2010        3
    ## 6        human  FALSE             1            2001           2002        1
    ## 7        chimp  FALSE             0            2003           2008        5
    ## 8        horse   TRUE             1            2008           2010        2
    ## 9          cat   TRUE             0            2009           2011        2

As can be seen, the mutate adds a new column to our dataframe which is
basically the difference between the 2 columns – gulo\_loss\_year and
sequencing\_year

### transmute()

Very similar to mutate but this will get rid of all other columns and
only show the new columns

``` r
transmute(gulo_df_new, time_gap = gulo_loss_year - sequencing_year)
```

    ##   time_gap
    ## 1        1
    ## 2        2
    ## 3        2
    ## 4        1
    ## 5        3
    ## 6        1
    ## 7        5
    ## 8        2
    ## 9        2

### summarise()

Summarise helps you to collapse dataframes into single rows by using
some functions that can aggregate results. A simple example is the mean
function

``` r
summarise(gulo_df, avg_sequencing_year = mean(sequencing_year))
```

    ##   avg_sequencing_year
    ## 1            2005.444

Intuitively this does not make sense because you just cannot take a mean
of years/dates. However, I want to stick to the same dataframe and do
not want to introduce a new dataframe just for the *summarise*
function.  
Secondly, the avg\_sequencing\_year does tell you that around this time
i.e. mid of 2005, most of these genome assemblies started to become
available.  
On a similar note, you could also make use of the *median* function
within *summarise*

``` r
summarise(gulo_df, median_sequencing_year = median(sequencing_year))
```

    ##   median_sequencing_year
    ## 1                   2006

### sample\_n() and sample\_frac()

Lastly, there are functions that help you take samples of
observations/rows from your dataframe. These functions are extremely
useful when you have a large dataframe consisting of many rows and you
only want to look at a subset of these observations.

``` r
sample_n(gulo_df, 5)
```

    ##        species status assembly_qual sequencing_year
    ## 1        chimp  FALSE             0            2003
    ## 2        horse   TRUE             1            2008
    ## 3          cat   TRUE             0            2009
    ## 4 kangaroo_rat   TRUE             1            2009
    ## 5   guinea_pig  FALSE             1            2006

In this case, the *sample\_n* function will return 5 rows randomly from
your dataframe. *sample\_frac* allows you to retrieve a fraction of your
sample instead of a fixed number of observations

``` r
sample_frac(gulo_df, 0.25)
```

    ##   species status assembly_qual sequencing_year
    ## 1   horse   TRUE             1            2008
    ## 2   chimp  FALSE             0            2003

This brings us to the end of the tutorial on dplyr package. As you have
seen, dplyr offers several functions to manipulate your dataframe and
remains extremely popular for these very reasons. In the next tutorial,
we will have a look at the pipe operator.
