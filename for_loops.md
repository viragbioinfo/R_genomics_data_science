Programming in R: for loops
================
Virag Sharma

We will now get to doing some more sophisticated stuff in R. We will
talk about the various possibilities you have in R to loop over elements
of your objects in R. This tutorial will be dedicated exclusively to the
**for** loop.

## FOR loop

If you have experience of programming in any other language, then you
would have heard of FOR loop before. It is perhaps the most primtive
concept you get taught as you learn about looping in R.

What does the for loop does? It basically allows you to iterate over all
the elements in your object. Here is an example of the for loop in
action:

``` r
my_vector <- 1:10
for (my_ele in my_vector) {
  print(my_ele)
}
```

    ## [1] 1
    ## [1] 2
    ## [1] 3
    ## [1] 4
    ## [1] 5
    ## [1] 6
    ## [1] 7
    ## [1] 8
    ## [1] 9
    ## [1] 10

Wow, we see the numbers getting printed from 1 till 10 on our screen.
But what did I do? Let us break this into individual steps:  
1\. I defined a vector called my\_vector that contains numbers from 1 to
10. Easy, peasy.  
2\. I used a *for* loop with this syntax: *for (my\_ele in
my\_vector)*  
This is followed by a an opening curly brace i.e. *{*, the print
statement (*print(my\_ele)*) and the closing curly brace i.e. *}*

So simply put, I defined a vector and then used a *for* loop.  
The most important bit of syntax here is: *for (my\_ele in
my\_vector)*  
We are basically pulling out each element from *my\_vector* during each
iteration or run of the loop. For each iteration, this element is stored
in the element called *my\_ele*.  
Once you understand this, the rest is pretty simple. Within the curly
braces, we define an action or a set of actions that needs to be
perfomed on every element. In the above example, we simply want to print
every element.

Let us do something that is a bit more complicated:

``` r
i <- 1
my_alphabets <- letters[1:10]
for (my_ele in my_alphabets) {
  print(paste("I am printing the element whose index is ", i, sep = ""))
  print(my_ele)
  i < i + 1
}
```

    ## [1] "I am printing the element whose index is 1"
    ## [1] "a"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "b"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "c"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "d"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "e"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "f"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "g"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "h"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "i"
    ## [1] "I am printing the element whose index is 1"
    ## [1] "j"

Here first of all, I defined a vector that contains alphabets from 1:10.
Note that R has an inbuilt vector of alphabets called letters. Here I
just pulled the first 10 letters out of it and placed it into the vector
*my\_alphabets*.  
I also initialzed a numeric object called *i* and set its value to 1.  
Then I begin my for loop, and notice that I have **two print
statements**.

The first print statement tells us that we are printing the element
whose index is *i*. This also explains the purpose of the the numeric
object *i*. Do not get confused by the print-paste combination, we will
learn more about it in the near future.

Then we print the element, increment the value of *i*, otherwise it
would be stuck at 1, and then we have the closing brace for the *for*
loop

Lastly, we can use for loop for all of the data structures we have
studied so far. We already saw that in action with a vector.

### 1\. *for* loop for matrices

``` r
r1 <- 1:5
r2 <- seq(10, 50, by = 10)
mat_row = rbind(r1, r2)
mat_row
```

    ##    [,1] [,2] [,3] [,4] [,5]
    ## r1    1    2    3    4    5
    ## r2   10   20   30   40   50

``` r
# Using for loop for printing every element in a matrix
for (ele in mat_row) {
  print(ele)  
}
```

    ## [1] 1
    ## [1] 10
    ## [1] 2
    ## [1] 20
    ## [1] 3
    ## [1] 30
    ## [1] 4
    ## [1] 40
    ## [1] 5
    ## [1] 50

We first constructed a matrix, and then used a for loop that printed
every single element of the matrix

### 2\. *for* loop for dataframes

``` r
c1 <- c(1,2,3,4,5)
c2 <- seq(10, 50, by = 10)
my_df <- data.frame(c1, c2)
my_df
```

    ##   c1 c2
    ## 1  1 10
    ## 2  2 20
    ## 3  3 30
    ## 4  4 40
    ## 5  5 50

``` r
# Using for loop for printing every column in the dataframe
for (ele in my_df) {
  print(ele)  
}
```

    ## [1] 1 2 3 4 5
    ## [1] 10 20 30 40 50

We first constructed a dataframe and were then able to run a for loop
that returns the two columns of a dataframe. Note that is different from
a matrix where you could retrieve every element

### 3\. *for* loop for lists

``` r
# Combining the dataframe and the matrix in a list
my_list = list(df = my_df, mat = mat_row)
my_list
```

    ## $df
    ##   c1 c2
    ## 1  1 10
    ## 2  2 20
    ## 3  3 30
    ## 4  4 40
    ## 5  5 50
    ## 
    ## $mat
    ##    [,1] [,2] [,3] [,4] [,5]
    ## r1    1    2    3    4    5
    ## r2   10   20   30   40   50

``` r
for (ele in my_list) {
  print(ele)
}
```

    ##   c1 c2
    ## 1  1 10
    ## 2  2 20
    ## 3  3 30
    ## 4  4 40
    ## 5  5 50
    ##    [,1] [,2] [,3] [,4] [,5]
    ## r1    1    2    3    4    5
    ## r2   10   20   30   40   50

Here we first constructed a list from the matrix and the dataframe that
we had created above. And then we ran a for loop to print every element
of the list. Since the list is composed of a matrix and a dataframe,
this is what we get back at the end.

Before we finish, the use of *for* loop also tells us how R thinks of
the building blocks of each of these datastructures.  
For a vector, it is obvious that R considers every element in a vector
as its constituent element.  
For a matrix, R considers every element in the matrix as the constituent
element of a matrix.  
For a dataframe, R considers every column in the dataframe as the
constituent element of the dataframe. This basically means R treats a
dataframe as a collection of columns.  
Lastly, we know that list is a datastructure that could be composed of
different datatypes. And this is exactly how R treats lists. In the
above example where we created a list from a matrix and a dataframe, the
for loop *decomposed* the list into a matrix and a dataframe.
