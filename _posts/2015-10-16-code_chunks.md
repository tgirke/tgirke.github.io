---
layout: post
title: Code Chunks 
---

{% highlight r %}
############################
## appendCounter Function ##
############################
## Author: Thomas Girke
## Last update: 03-Oct-15

## Function to append occurrence counter to entries in character 
## vector and return the results as named vector where the 
## original data are in the same order in the data slot
## and the counting result in the name slot.
appendCounter <- function(x, sep="_") {
    names(x) <- sprintf(paste0("%0", as.character(nchar(length(x))+1), 
                        "d"), seq_along(x))
    tmp <- sort(x)
    f <- table(tmp)
    tmp2 <- unlist(sapply(names(f), function(z) paste(z, 1:f[z], 
                   sep=sep)))
    names(tmp2) <- names(tmp)
    names(x) <- tmp2[sort(names(tmp2))]
    return(x)
}
## Usage:
x <-  c("a", "b", "c", "b", "h", "c")                                            
appendCounter(x, sep="_")
{% endhighlight %}

