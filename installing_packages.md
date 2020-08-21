Installing packages in R
================
Virag Sharma

So far we have not used an external R package. If you are wondering what
an external package is, you first need to understand the concept of a
**built-in** function.  
A built-in function in R is something that is available to use the
moment you have installed R on your system.

A simple example is the *rep* function that we have discussed in the
tutorial on vectors. You might remember that you just typed rep in your
console and you could use it. It is an built-in function because you
simply call it from your R-console.

However, note that any programming language can only have a finite
number of built-in functions. With time people will want to do newer
things with a programming language and in very simple words, this will
demand more built-in functions. Of course, new functionalities do get
added to R with every new release. But you do not want to wait for a new
release all the time. To overcome these limitations, people write their
own packages that contain the desired functionality. An end-user is
required to install this package first. If the package is successfully
installed, then the user can simply load this package and call functions
that are a part of this package.

Let us see how to install packages first. Installing a package is
perhaps one of the easiest things to do in R. On your R-console, you
just need to type the following:

``` r
# install.packages(your_package_name)
```

You might be asked on which mirror you want to use. Just select the one
that is closer to you geographically. This will trigger a series of
outputs in your R-console but basically indicates the progress of the
installation. Once the installation is complete, you will need to load
this package every time you want to call the functions that this package
provides.

Note that the install.packages function will work only if you are
installing packages from CRAN. CRAN is the standard R package repository
where people submit their packages. Also note that all packages relevant
for computational biology may not be available from CRAN but more odten
than not they are available via BiocManager.

BiocManager can be installed in the manner that I have described above

``` r
# install.packages("BiocManager")
```

Once BiocManager is installed, you need to load this package and then
use the install function of BiocManager to install computational biology
relevant packages

``` r
# library("BiocManager")
# install("DESeq2")
```

### The double colon notation

Sometimes, you might observe that to install a package using
BiocManager, such as DESeq2, people will use the following notation

``` r
# library("BiocManager")
# BiocManager::install("DESeq2")
```

The **BiocManager::** that is prefixed to the install function tells R
to specifically use the install function from the BiocManager package.
Why would this matter?  
This matters because it is also possible that you have written you own
*install* function for some other purpose (we will learn more about
writing our own functions later). This might clash with the install
function from BiocManager.  
By prefexing the name of the package, you are making this explicitly
clear to R that you want to use the install function from BiocManager
only.  
It is generally considered a **good programming practise** in R to
specify the name of the package before calling the function using the
double colon notation.

### Other ways of installing packages

Sometimes you might need to install a function that is not available on
CRAN but is available in a public git repository. This can be installed
using the install\_github function from the devtools library. First, you
need to install the devtools package. Subsequently, you use the
install\_github function

``` r
# install.packages("devtools")
# library(devtools)
# devtools::install_github(name_of_git_repository)
```

There are other ways of installing a package such as installation from
the source code of a package but they are less commonly used.
