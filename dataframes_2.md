DATAFRAMES: Part 2
================
Virag Sharma

### Operations with dataframes

Let us create a dataframe that contains two columns: a list of species
and a logical informing us whether a particular gene (Gulo) is present
in the species or not (Reference: Hiller *et al.* 2012 Pubmed ID:
23022484)

``` r
species <- c('mouse', 'rat', 'kangaroo_rat', 'guinea_pig', 'rabbit', 'human', 'chimp', 'horse', 'cat')
status <- c(T, T, T, F, T, F, F, T, T)
gulo_df <- data.frame(species, status)
gulo_df
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

Another useful in-built function is *str*. It gives you the idea about
the structure of the dataframe

``` r
str(gulo_df)
```

    ## 'data.frame':    9 obs. of  2 variables:
    ##  $ species: Factor w/ 9 levels "cat","chimp",..: 7 9 6 3 8 5 2 4 1
    ##  $ status : logi  TRUE TRUE TRUE FALSE TRUE FALSE ...

As expected, you see that gulo\_df is a dataframe that has two
variables. The ‘status’ variable is logical but the ‘species’ variable
is a factor which is what we do not want.  
Before we convert this to a character, note that R has the default
option of treating characters as factors unless explicity told
otherwise.  
Let us convert the datatype of the species variable from factor to
character

``` r
gulo_df$species <- as.character(gulo_df$species)
```

To see if this worked, let us check the structure of the dataframe

``` r
str(gulo_df)
```

    ## 'data.frame':    9 obs. of  2 variables:
    ##  $ species: chr  "mouse" "rat" "kangaroo_rat" "guinea_pig" ...
    ##  $ status : logi  TRUE TRUE TRUE FALSE TRUE FALSE ...

As you can see the datatype of the species variable is now indicated as
chr which stands for character.  
Alright, now that we have dataframe, we will do some operations on the
dataframe.

### 1\. Adding columns to an existing dataframe

Suppose we have information about the genome assemblies of the species
that we have in our gulo\_df dataframe and we want to add this
information to the dataframe The assembly quality looks like the
following

``` r
assembly_qual <- c(1, 1, 1, 1, 1, 1, 0, 1, 0)
```

Expectedly this is also a vector with 9 values. Each number (0 or 1)
corresponds to the quality of the genome assembly of the species listed
in our original dataframe. 1 refers to a good quality (implying that we
can be reasonably certain that the Gulo gene is intact or non-intact in
the species) while 0 refers to questionable quality, implying that we
cannoy confidently say whether the gene is intact or non-intact in the
species

There are two ways to add a column to an existing dataframe. We can use
the standard *data.frame* function

``` r
gulo_df_new <- data.frame(gulo_df, assembly_qual)
gulo_df_new
```

    ##        species status assembly_qual
    ## 1        mouse   TRUE             1
    ## 2          rat   TRUE             1
    ## 3 kangaroo_rat   TRUE             1
    ## 4   guinea_pig  FALSE             1
    ## 5       rabbit   TRUE             1
    ## 6        human  FALSE             1
    ## 7        chimp  FALSE             0
    ## 8        horse   TRUE             1
    ## 9          cat   TRUE             0

Note that we have create a new dataframe (gulo\_df\_new) here but we
could have updated the existing dataframe as well

``` r
gulo_df <- data.frame(gulo_df, assembly_qual)
gulo_df
```

    ##        species status assembly_qual
    ## 1        mouse   TRUE             1
    ## 2          rat   TRUE             1
    ## 3 kangaroo_rat   TRUE             1
    ## 4   guinea_pig  FALSE             1
    ## 5       rabbit   TRUE             1
    ## 6        human  FALSE             1
    ## 7        chimp  FALSE             0
    ## 8        horse   TRUE             1
    ## 9          cat   TRUE             0

Another way to add a column to a dataframe is by using the **$**
notation but with this, you can only **‘add’** columns to an existing
dataframe and there can be no assignment a different data-frame Let’s
recreate the gulo\_df that does not have the assembly\_quality
column

``` r
species <- c('mouse', 'rat', 'kangaroo_rat', 'guinea_pig', 'rabbit', 'human', 'chimp', 'horse', 'cat')
status <- c(T, T, T, F, T, F, F, T, T)
gulo_df <- data.frame(species, status)
```

Here is how we can append columns using the $ notation

``` r
gulo_df$assembly_qual <- assembly_qual
```

Note that the following won’t work

``` r
gulo_df_new$assembly_qual <- assembly_qual
```

### 2\. Adding rows to an existing dataframe

To add new rows to an existing dataframe, we need to make use of the
*rbind* function Let us say, we got information about another species
(the famous naked mole rat) and we want to add this to the gulo\_df
dataframe

``` r
nmr_info <- c('naked_mole_rat', TRUE, 1)
```

Adding this information requires using the *rbind*
    function

``` r
gulo_df_appended <- rbind(gulo_df, nmr_info)
```

    ## Warning in `[<-.factor`(`*tmp*`, ri, value = "naked_mole_rat"): invalid factor
    ## level, NA generated

``` r
gulo_df_appended
```

    ##         species status assembly_qual
    ## 1         mouse   TRUE             1
    ## 2           rat   TRUE             1
    ## 3  kangaroo_rat   TRUE             1
    ## 4    guinea_pig  FALSE             1
    ## 5        rabbit   TRUE             1
    ## 6         human  FALSE             1
    ## 7         chimp  FALSE             0
    ## 8         horse   TRUE             1
    ## 9           cat   TRUE             0
    ## 10         <NA>   TRUE             1

Note that since the vector (nmr\_info) is supposed to contain different
data types (character, logical and numeric) and they were all converted
to character, the datatypes for status and assembly\_qual have also been
changed to character in the resulting dataframe

``` r
str(gulo_df_appended)
```

    ## 'data.frame':    10 obs. of  3 variables:
    ##  $ species      : Factor w/ 9 levels "cat","chimp",..: 7 9 6 3 8 5 2 4 1 NA
    ##  $ status       : chr  "TRUE" "TRUE" "TRUE" "FALSE" ...
    ##  $ assembly_qual: chr  "1" "1" "1" "1" ...

To fix this, we need to do the following:

``` r
gulo_df_appended$status <- as.logical(gulo_df_appended$status)
gulo_df_appended$assembly_qual <- as.numeric(gulo_df_appended$status)
str(gulo_df_appended)
```

    ## 'data.frame':    10 obs. of  3 variables:
    ##  $ species      : Factor w/ 9 levels "cat","chimp",..: 7 9 6 3 8 5 2 4 1 NA
    ##  $ status       : logi  TRUE TRUE TRUE FALSE TRUE FALSE ...
    ##  $ assembly_qual: num  1 1 1 0 1 0 0 1 1 1

Sanity restored :)
