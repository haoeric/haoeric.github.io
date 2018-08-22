---
layout: postDataAnalysis
title: Extremely Fast Row Match between Two Matrixes using data.table
comments: true
categories: [Data Analysis]
tags: [R, data.table, match]
---


Even though I have heared about [data.table](https://cran.r-project.org/web/packages/data.table/index.html) many times, but this is the first time I tasted the sweetness of it. It's really fast.

My problem is to compare rows between two matrix and get the match ID. More exactly, I want a function to match matrix x to matrix y by rows, then return the match ID of y.

My first idea was to claculate the distance between rows of matrix x and matrix y. To solve the memory limit for big distance matrix, I cut matrix x into chunks. Without *data.table*, I wrote a funciton like this below:

```R

rowMatch <- function(x,y){
    mid <- NULL
    colm <- match(colnames(x), colnames(y))
    if(any(is.na(colm)) || ncol(x) != ncol(y)){
        stop("colnames doesn't match!")
    }
    y <- y[ ,colm]
    
    splitFactor <- splitFactorGenerator(nrow(x), nrow(y))
    dataFolds <- split.data.frame(as.data.frame(x), splitFactor)
    
    for(k in 1:length(dataFolds)){
        cat("Fold ", k , " in ", length(dataFolds), ", ")
        xk <- as.matrix(dataFolds[[k]])
        cat(nrow(xk), "cells  \n")
        xydist <- as.matrix(pdist::pdist(xk, y))
        cat('Distance done\n')
        for(i in 1:nrow(xk)){
            xim <- which(xydist[i,] == 0)
            if(length(xim) == 0){
                message("Row ", i, " has no match in y!")
            }
            mid <- c(mid, xim)
        }
        cat('Match done\n\n')
    }
    
    mid <- unique(mid)
    if(length(mid) == nrow(x)){
        cat("x completely match in y.\n")
    }else{
        cat("Match percentage: ", round(length(mid)/nrow(x),2) * 100, "%.\n")
    }
    
    return(mid)
} 

## generate split factors to split rowNum into folds, each of size around foldSize
splitFactorGenerator <- function(rowNum, colNum){
    if(missing(colNum)){
        colNum <- rowNum
    }
    foldSize <- round(62772663 / colNum)  ## each chunk with maxi 500Mb
    foldNum <- ceiling(rowNum / foldSize)
    lastfoldSize <- rowNum - (foldNum-1) * foldSize
    if(foldNum > 1){
        splitFactor <- c(rep(1:(foldNum-1), each = foldSize), rep(foldNum, lastfoldSize))
    }else{
        splitFactor <- rep(foldNum, lastfoldSize)
    }
    return(splitFactor)
}
```

But this is fairly slow, especially when the matrix is big. So I started to search for some fast methods. I found this similar question on [stackoverflow](http://stackoverflow.com/questions/9316946/comparing-rows-between-two-matrices) which shows the usage of *data.table*. But that doesn't return the original ID of y, so I modified a little bit to get my second version of `rowMatch` as below:

```R
require(data.table)
rowMatch2 <- function(x,y){

  colm <- match(colnames(x), colnames(y))
    if(any(is.na(colm)) || ncol(x) != ncol(y)){
        stop("colnames doesn't match!")
    }
  
  keycols <- colnames(x)[colm]
  x <- cbind(x, id=1:nrow(x))
  y <- cbind(y, id=1:nrow(y))
  m1 = data.table(x)
  setkeyv(m1, keycols)
  m2 = data.table(y)
  setkeyv(m2, keycols)
  m1id <- m1$id
  m2id <- m2$id
  
  m1$id <- NULL
  m2$id <- NULL
  
  m <- na.omit(m2[m1,which=TRUE])
  mo <- m2id[m][order(m1id)]
  
  if(length(mo) == nrow(x)){
    cat("Complete match!\n")
  }else{
    cat("Uncomplete match, match percentage is:", round(length(mo)/nrow(x), 4)*100, "%\n")
  }
  return(as.integer(mo))
}
```

It's incrediablely fast, I will figure it out and really need to equip with this hack tool for data manipulation.