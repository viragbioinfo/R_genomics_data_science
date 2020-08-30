The break statement
================
Virag Sharma

We have previouly discussed two ways of looping in R. One of them
involves the use of *for* loop while another way of looping is using the
*while* loop/statement.  
However, we may be faced with a scenario where we would like to break
out of the loop for some reason. The *break* statement allows us this
fuctionality.

### Using *break* with *while* loop

``` r
i <- 2
while (i <= 10) {
  cat('The value of our variable i is', i, '\n')
  i <- i + 2
  if (i == 8) {
    cat('The value of our variable i is', i, 'which is where we intended to break out of the loop\n')
    break
  }
}
```

    ## The value of our variable i is 2 
    ## The value of our variable i is 4 
    ## The value of our variable i is 6 
    ## The value of our variable i is 8 which is where we intended to break out of the loop

In the above code, we started by setting the value of our variable *i*
to 2 and incrementing it by 2 in every iteration. According to the while
loop, we have set a condition that *i* must reach 10 before we exit out
of loop.  
However, note we have added another *if* condition where we ask if *i*
is equal to 8. If yes, then we print a statement and then break out of
the loop.

### Using *break* with *for* loop

Similarly, we can use the *break* statement to exit out of a *for* loop.

``` r
my_vec <- 1:10
for (my_ele in my_vec) {
  cat('The value of our element i is', my_ele, '\n')
  if (my_ele == 5) {
    cat('Exiting the for loop at this point')
    break
  }
}
```

    ## The value of our element i is 1 
    ## The value of our element i is 2 
    ## The value of our element i is 3 
    ## The value of our element i is 4 
    ## The value of our element i is 5 
    ## Exiting the for loop at this point
