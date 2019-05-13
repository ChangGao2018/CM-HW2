# CM-HW2
---
title: "Simple neural networks"
author: "Chang Gao"
date: "Date of submission"
output: 
  html_document: 
    highlight: tango
    theme: spacelab
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(tidyverse)

theme_set(theme_classic(base_size = 16))
```

* * *

The XOR function
```{r xor_values}
xor_input <- crossing(x1 = c(0, 1), 
                       x2 = c(0,1))

xor_output <- xor_input %>%
  transmute(y = as.numeric(xor(x1, x2))) %>%
  pull(y)
```

A helper function for tidying up perceptron output
```{r tidy-perceptron-output}
tidy_perceptron <- function(errors, weights, inputs, iterations) {
  
 # Get weights and errors into a tidy form
  tidy_errors <- errors %>% 
    bind_cols() %>% 
    t %>%
    as_data_frame() %>%
    mutate(iteration = 1:n()) %>%
    gather(train, error, -iteration) %>%
    mutate(train = gsub("V", "", train)) %>%
    mutate(train = as.numeric(train))

  tidy_weights <- weights %>% 
    bind_cols() %>% 
    t %>%
    as_data_frame() %>%
    select_all(~gsub("V", "weight", .)) %>%
    slice(-1) %>%
    mutate(train = rep(1:nrow(inputs), iterations)) %>%
    group_by(train) %>%
    mutate(iteration = 1:n())
  
  return(left_join(tidy_weights, tidy_errors, 
                   by = c("train", "iteration")))
}
```

Write the perceptron learning function
```{r perceptron}
perceptron <- function(inputs, outputs, rate, iterations) {
  
  # initialize weight vector
  weights <- c(rep(0, ncol(inputs) + 1)) %>% # what is this extra +1 for? 
    list() 
  # initialize an empty errors list
  errors <- list()
        
   # for each iteration
  for (iteration in 1:iterations) {
    error <- rep(0, nrow(inputs)) # to fill in
  
    # for each training example
    for (train in 1:nrow(inputs)) {
     
      # get the weight after the last exemplar
       weight <- last(weights) %>% 
         unlist()
      
       # Predict output label using Heaviside activation 
      ouput <- 
                
      # Update weights
      weight <- 
      
      # store the weights
      weights <- c(weights, as_data_frame(weight))
      
      # Compute error
      error[train] <- 
    }
    
    #store the error
    errors <- c(errors, as_data_frame(error))
    
    }
  
  # Get weights and errors into a tidy form
   return(tidy_perceptron(errors, weights, inputs, iterations))
}
```

Examine perceptron weights and errors
```{r perceptron-output}

```

Backprop network
```{r backprop}

```

Examine backprop network weights and errors
```{r backprop}

```


Elman network
```{r backprop}

```

Examine Elman network weights and errors
```{r test_plots}

```

