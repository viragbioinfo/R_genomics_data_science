R: The fundamentals
================
Virag Sharma

Welcome to the **R course for genomics data science**. As you could
probably guess from the title of the course, there will be three things
covered in this course, all of which are pretty **hot** right now. These
include R, genomics and data science.

### Brief background

R is a modern programming language that continues to soar in its
popularity. The project was conceived in 1992, with an initial version
released in 1995 and a stable beta version (v1.0) on 29 February 2000.
(source wikipedia). At the time of writing this document, the most
recent version of R is 4.0.2.

The field of Genomics pretty much started with this millenium as the
first draft of the human genome became available. Since then, the
progress in this field has been tremendous. Especially with the advent
of newer sequencing technologies that are faster and cheaper than their
predecessors, the amount of sequence data has grown at an unprecedented
pace.

Lastly, Data Sciene is a very popular area of science these days.
Basically Data Science involves the analyses of data (in the current
context, we are talking about sequencing data mostly) using robust
statistical frameworks and arriving to conclusions that are
statistically significant.

We will first learn some basics of R and then move to some
domain-specific applications of R.

### RStudio

During this course, we will make use of RStudio. RStudio provides a nice
interface to the R programming language. But please note that RStudio
just provides a friendly interface to the R language and nothing more.
The actual computation is done by the language which is R, and the
syntaxt of the language has to be followed regardless of whether you are
typing your code in R studio or writing code for a standalone Rscript.
Below is a screenshot showing the console of the Rstudio ![R
studio](Rstudio_screenshot.png)

As you can see your screen seems to be split into 3 sections across 2
columns. The column on the left, also called as **Console** is the one
we will be using to key in all R commands/code. We will make use of the
other panels in due course.

### R objects

To illustrate the concept of objects in R, let us just start with a
simple example

``` r
x = 2
x
```

    ## [1] 2

What we have done above is simply assing the numeric value 2 to x. But
what exactly is x here? x is essentially some slot in the memory of your
computer that holds this value. A more common notation that can be used
in this case is simply addressing x as a variable.

While “x = 2” does the job, the R-specific way of object assignment
makes use of the less-than symbol followed by a minus sign

``` r
x <- 2
```

To confirm if R does indeed store the value 2 in the object x, just type
in x in your console

``` r
x
```

    ## [1] 2

However, keep in mind that you have to be careful of these assignment
operations. You could also easily overwrite this value and R would not
even warn you of the re-assignment opertion you did

``` r
x
```

    ## [1] 2

``` r
x <- 10
x
```

    ## [1] 10

As we can see, x is now holding a value of 10 and as we flipped from the
old value (2) to the new value (10), we did not get any warning.

### Naming objects in R

A quick note about how you name your objects. Some people prefer using
short names for their objects (which may be useful but non-intuitive),
some people prefer using camelcase (see examples), some use underscores
and lastly some use dots in their variable name.  
This is essentially a matter of choice and while there are no strict
recommendations, it is generally recommended that you use one naming
convention and then stick to it throughout your code to ensure better
readibility and understanding of your
code

``` r
# you would not really know what is being discussed here, so this is a non-intuitive name for your object
g_length <- 100
# using camelCase, this is fairly intuitive
geneLength <- 100
# using underscores, this is also fine
gene_length <- 100
# using dots, this is also fine
gene.length <- 100
```

Lastly, note that these names are case-sensitive. So gene\_length is not
the same as gene\_Length

### Different datatypes in R

We have learnt that we can assign values to different objects in R. Note
that these values can differ, not only in terms of what values they are
but also in terms of their type.  
For instance

``` r
var_1 <- 100
var_2 <- 'I am a Bioinformatician'
```

It is obvious that var\_1 contains a value that is numeric in nature
while var\_2 contains something that is textual in nature.  
To determine the nature of a datatype, there are two in-built functions
*class* and *typeof*

``` r
var_1 <- 100
class(var_1)
```

    ## [1] "numeric"

``` r
typeof(var_1)
```

    ## [1] "double"

``` r
## Now with the textual string
var_2 <- 'I am a Bioinformatician'
class(var_2)
```

    ## [1] "character"

``` r
typeof(var_2)
```

    ## [1] "character"

You will observe that for var\_1, the function *class* returns
**numeric** while the function *typeof* return **double** which is a
more-specific subtype of numeric.  
For var\_2, both the functions return **character** which is in
accordance with our expectations.

### Different data structures in R

So far we have discussed objects in R. An object is essetially a
variable that holds a certain value. However, more often than not, we
will need to store multiple values in an object and not just a single
value. Hence, we will need to make use of different data structures in
R.  
The most commonly used data structures in R are:  
1\. Vector  
2\. Matrix  
3\. Dataframe  
4\. List

In the subsequent tutorials, we will go through these data structures
and learn the finer nuances of each of these data structures.
