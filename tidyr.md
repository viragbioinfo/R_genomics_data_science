The tidyr package
================
Virag Sharma

We have previously discussed the dplyr package that helps us perform
various operations on our dataframe. Here we are going to be learn the
**tidyr** package.

As the name suggests, the package is useful for **tidying up** your
data.  
According to the developers of the package, tidy data is the data that
is amenable to standard operations using dplyr or can be easily
visualised using ggplot2.  
The two salient features of tidy data are the following:  
1\. Each column is a variable 2. Each row is an observation

This setup makes your life easier because it provides a consistent
framework – everytime you have to refer to a variable, you call the
column name. Similarly, every time you have to call an observation, you
call it by its row-name or the index.  
Let us look at an example for better understanding of the concepts of
tidyr.

``` r
dataframe_messy <- data.frame(genes = c('FOXP3', 'IL7RA', 'ZBED2'), counts_disease = c(100, 110, 107), counts_normal = c(700, 638, 695))
dataframe_messy
```

    ##   genes counts_disease counts_normal
    ## 1 FOXP3            100           700
    ## 2 IL7RA            110           638
    ## 3 ZBED2            107           695

In the above example, I have made up some information that seems to come
from an RNAseq study. There are three genes of interest and there are
two columns – one reflects the expression of these genes in diseased
condition while the other column reflects the expression of these genes
in normal conditions.  
Note that this is a not a tidy format because we actually have only one
variable **counts** but it is expressed in two different columns.

The **tidyr** package has the functionality to make this data tidy for
us. Let us start with the first function from the package.

However, do install the **tidyr** package if you have not already
installed

``` r
# I am not doing it since I have already installed the package
#install.packages('tidyr')
```

### gather

The gather function allows us to gather the same variable from different
columns like the example we have above

``` r
library(tidyr)
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
dataframe_messy %>% gather(condition, counts, counts_disease, counts_normal)
```

    ##   genes      condition counts
    ## 1 FOXP3 counts_disease    100
    ## 2 IL7RA counts_disease    110
    ## 3 ZBED2 counts_disease    107
    ## 4 FOXP3  counts_normal    700
    ## 5 IL7RA  counts_normal    638
    ## 6 ZBED2  counts_normal    695

As you can see above, *gather* converts the data from a **wide** to a
**long** format. The first argument to the gather function is the name
of the variable that you will use to group the two columns (condition -
whether diseased or normal), the second argument is the name of the
actual variable that you determined (thec counts). This is followed by
the names of the columns from our original dataframe that were grouped
(counts\_disease, counts\_normal).

Let us try another dataframe with more columns and try to group them
using
gather

``` r
dataframe_messy <- data.frame(genes = c('FOXP3', 'IL7RA', 'ZBED2'), counts_R1 = c(800, 110, 250), counts_R2 = c(700, 114, 272), counts_R3 = c(723, 156, 321))
dataframe_messy
```

    ##   genes counts_R1 counts_R2 counts_R3
    ## 1 FOXP3       800       700       723
    ## 2 IL7RA       110       114       156
    ## 3 ZBED2       250       272       321

``` r
dataframe_messy %>% gather(replicate, counts, counts_R1, counts_R2, counts_R3)
```

    ##   genes replicate counts
    ## 1 FOXP3 counts_R1    800
    ## 2 IL7RA counts_R1    110
    ## 3 ZBED2 counts_R1    250
    ## 4 FOXP3 counts_R2    700
    ## 5 IL7RA counts_R2    114
    ## 6 ZBED2 counts_R2    272
    ## 7 FOXP3 counts_R3    723
    ## 8 IL7RA counts_R3    156
    ## 9 ZBED2 counts_R3    321

``` r
# Use the colon notation to specify the columns that are being grouped
dataframe_messy %>% gather(replicate, counts, counts_R1:counts_R3)
```

    ##   genes replicate counts
    ## 1 FOXP3 counts_R1    800
    ## 2 IL7RA counts_R1    110
    ## 3 ZBED2 counts_R1    250
    ## 4 FOXP3 counts_R2    700
    ## 5 IL7RA counts_R2    114
    ## 6 ZBED2 counts_R2    272
    ## 7 FOXP3 counts_R3    723
    ## 8 IL7RA counts_R3    156
    ## 9 ZBED2 counts_R3    321

As you have seen now, you could also use the colon notation to specify
the columns that you want to group.

### spread

The spread function allows us to spread the values in our dataframe and
convert it from *wide* to *long* format. This may seem like
**untidying** our data again but this may be needed sometimes. A typical
application is the case when you need to make a scatter plot. So even
though you have the same kind of values on both x and y axis, they need
to be split into two distinct columns. Here is an example:

``` r
# create a dataframw with an additional column called total_read_count
dataframe_tidy <- data.frame(cell_id = c('cell1', 'cell2', 'cell3', 'cell1', 'cell2', 'cell3'), counts_type = c('ERCC', 'ERCC', 'ERCC', 'total_counts', 'total_counts', 'total_counts'), counts = c(800, 760, 14000, 1000000, 1000020, 1000200))
```

Now this dataframe confirms to our definition of the tidy data. Each
column corresoonds to a variable in our data and there is clearly a
key-value relationship between the different elements of our dataframe.
However, if you were to plot a scatterplot that shows the counts for
ERCC spike-ins on one axis and total number of counts on another axis
(useful to identify outlier cells), then you cannot simply do this
operation with this dataformat without processing your dataframe.
*spread* comes to your rescue here.

``` r
dataframe_tidy %>% spread(counts_type, counts)
```

    ##   cell_id  ERCC total_counts
    ## 1   cell1   800      1000000
    ## 2   cell2   760      1000020
    ## 3   cell3 14000      1000200

As you can see, *spread* splits the counts\_type column into two
distinct columns called ERCC and total\_counts and produces a 3 X 3
dataframe.

### separate

The *separate* function is a convenience function to separate a column
into two or more distinct columns. Here is an
example:

``` r
my_dataframe <- data.frame(cell_id = c('cell_1', 'cell_2', 'cell_3'), cell_info = c('K562_cognate', 'K562_cognate', 'PBMC_mock'), library_count = c(1000000, 1000100, 1000200))
```

In this dataframe, the column *cell\_info* contains condensed
information from two different variables – the cell type whether it is
K562 or PBMC, and the stimulation – whether it is the cognate peptide or
the mock one. We can split apart this column into two columns using
*separate*

``` r
my_dataframe %>% separate(cell_info, c("cell_type", "stimulation"))
```

    ##   cell_id cell_type stimulation library_count
    ## 1  cell_1      K562     cognate       1000000
    ## 2  cell_2      K562     cognate       1000100
    ## 3  cell_3      PBMC        mock       1000200

Now you see the column *cell\_info* split into two columns -
*cell\_type* and *stimulation*. A more elegant way of using separate is
the
following:

``` r
my_dataframe %>% separate(col = cell_info, into = c("cell_type", "stimulation"), sep = '_')
```

    ##   cell_id cell_type stimulation library_count
    ## 1  cell_1      K562     cognate       1000000
    ## 2  cell_2      K562     cognate       1000100
    ## 3  cell_3      PBMC        mock       1000200

Here we explicitly specify that we are splitting the column *cell\_info*
into 2 columns – *cell\_type* and *stimulation*, and the separator we
want is an underscore i.e. \*\_\*

### unite

The *unite* function, as the name suggests is exactly the opposite of
*separate*. It allows you to group two variables/columns into a single
variable. Here is an
example:

``` r
my_dataframe <- data.frame(cell_id = c('cell_1', 'cell_2', 'cell_3', 'cell_4'), cell_type = c('K562', 'K562', 'PBMC', 'PBMC'), stimulation = c('cognate', 'cognate', 'mock', 'mock'), library_count = c(1000000, 1000100, 1000200, 100300))
my_dataframe
```

    ##   cell_id cell_type stimulation library_count
    ## 1  cell_1      K562     cognate       1000000
    ## 2  cell_2      K562     cognate       1000100
    ## 3  cell_3      PBMC        mock       1000200
    ## 4  cell_4      PBMC        mock        100300

``` r
my_dataframe %>% unite(cell_info, c('cell_type', 'stimulation'), sep = '_')
```

    ##   cell_id    cell_info library_count
    ## 1  cell_1 K562_cognate       1000000
    ## 2  cell_2 K562_cognate       1000100
    ## 3  cell_3    PBMC_mock       1000200
    ## 4  cell_4    PBMC_mock        100300

This brings us to the end of this tutorial. To summarise, we learnt
about 4 operations here: 1. Converting data from wide to long format -
use *gather*.  
2\. Converting data from long to wide format - use *unite*.  
3\. Splitting a column/variable into two (or more) invidual variables -
use *separate*.  
4\. Merging two or more columns/variables into a single variable - use
*unite*
