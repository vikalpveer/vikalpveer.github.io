---
layout: post
title: "Insertion Sort Algorithm - Implementation and Analysis"
date: "2018-09-11"
slug: "insertion-sort"
description: "Insertion Sort is a simple in-place comparison based sorting Algorithm"
category:
  - Algorithm
# tags will also be used as html meta keywords.
tags:
  - Algorithm
  - Sorting
show_meta: false
comments: true
mathjax: true
mermaind: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
---
Let $$A$$ be an array of length $$len$$ . Insertion sort is another comparison based algorithm to sort the array so that resulting array is $$ A[0] \leq A[i] \leq [len-1] \ \forall \ i  \in [0,1,2.., len-1]$$. 
<!--more-->

In insertion sort, element at current index $$k$$  where $$ 0 \leq k \leq len-1$$ is compared with all elements in the left and inserted at the location such that resulting subarray from index $$0$$ to $$k$$ is sorted.  

### Python Implementation

```python
    def InsertionSort(self, A):
        l = len(A)
        # Outer For loop going through each element
        for i in range(0, l):
            key = A[i]
            j = i -1
            # Inner loop comparing all elements 
            #left of current element and greter than
            #current element.
            while j >=0 and A[j] > key:
                    A[j + 1] = A[j]
                    j = j -1       
            A[j+1] = key

```



Analysing the algorithm, we can see that the outer loop runs through the length of the array. If array is already sorted (best case), then inner loop will not execute at all and the complexity of the algorithm would be $$\theta(n)$$. On the other hand, if the given array is in a descending order, then for each outer element, algorithm would execute inner loop and compare all the elements in the left resulting in the worst case complexity of $$\theta(n^{2})$$

If the elements of the array are randomly chosen, the inner loop is expected to execute half of the time, resulting in average case running time of insertion sort to be $$\theta(n^{2})$$

Insertion sort is usually used for sorting when the size of the array is very small (less than or equal to 5) becuase in this case the average complexity of the algorithm is linear i.e $$\theta(n)$$


