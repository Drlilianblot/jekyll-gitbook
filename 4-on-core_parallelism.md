---
title: 4. On-Core Parallelism
date: 2022-07-24
category: hipc
layout: post
---

# Overview




Over the next three units we're going to be looking at how to develop applications for homogeneous distributed systems. In this unit, we're going to start with performance and parallelism at the core level. 

Specifically we're going to cover: 

* Some really simple optimisations
* Some slightly less obvious optimisations
* Optimising iterative code (loops)
* Writing vectorised code
* Having the compiler write vectorised code
 


## Shrink The Working Set

The _working set_ of an application is the amount of memory it uses. Generally, if we can reduce the amount of memory an application uses, we can likely improve its performance by raising the probability of cache hits. One simple way to do this is to consider the storage required for each variable. 

In the example above, double precision is used for the floating-point values, meaning that each value occupies 8 bytes (64 bits). If this level of precision is not required, we could replace `double` with `float` and reduce our working set by a half. This may also be advantageous since single-precision calculations are usually cheaper than double-precision ones! 

The important thing to consider is what precision is required, and whether switching precision will change any other properties of your application (e.g. will it affect convergence of a calculation). 
 
> **Further Reading** 
>
> * [Introduction to High Performance Computing for Scientists and Engineers](https://yorsearch.york.ac.uk/permalink/f/1d5jm03/44YORK_ALMA_DS51308825180001381), Section 2.2 Common Sense Optimizations
{: .block-tip }

# More Simple Optimisations
     
So, we've covered some common sense general optimisations. Now we'll look at some more simple optimisations that can have a large impact on performance. Many of these optimisations may be performed by your compiler already -- but again, the easier we make it for the compiler, the better. 

## Eliminate Common Subexpressions



<iframe width="560" height="315" class="center" src="https://www.youtube.com/embed/Yx7_i8wx2sc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe> 


