---
layout: post
title: "Comparison of Quadratic Run time Sorting Algorithm"
date: "2018-09-14"
slug: "compare-quadratic-complexity-sort-algo"
description: "Comparing performance of Quadratic Rum Time Complexity Algorithm: Comparing performance of Bubble Sort, Selection Sort and Insertion Sort"
category:
  - Algorithm
# tags will also be used as html meta keywords.
tags:
  - Algorithm
  - Array
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

Bubble Sort, Selection Sort and Insertion Sort are all Quadratic Time Complexity sorting algorithms i.e their average time complexity is $$\theta(n^{2})$$ . However, we often read insertion sort performs better than the two other $$\theta(n^{2})$$ algorithms. Let's analyse the reason behind this and compare the performance of these three algorithms. 

<!--more-->
First let's have a look at the implementation of these three algorithms.

### Bubble Sort

```python
def BubbleSort(self, data)
    not_sorted = True
    l = len(data)
    while not_sorted:
        not_sorted = False
        for i in range(l - 1):    
            if data[i] > data[i+1]:
                data[i], data[i+1] = data[i+1], data[i]
                not_sorted = True
```

### Selection Sort

```python
def SelectionSort(self,data):
    for i in range(len(data)):
        min_idx = i
        for j in range(i+1, len(data)):
            
            if(data[min_idx] > data[j]):
                min_idx = j
        if(min_idx != i):
            data[i], data[min_idx] = data[min_idx], data[i]
```

### Insertion Sort

```python
def InsertionSort(self,data):
    l = len(data) 
    # Outer For loop going through each element
    for i in range(0, l):
        key = data[i]
        j = i -1
        # Inner loop comparing all elements 
        #left of current element and greter than
        #current element.
        while j >=0 and data[j] > key:
                
                data[j + 1] = data[j]
                j = j -1       
        data[j+1] = key
```



If we analyse the above three algorithms, we can notice that all three algorithm runs two loops but the key to the performance of the three algorithms lies in the optimisation done in the inner loop. In case of bubble sort and selection sort, both algo runs through same number of iterations but bubble sort performs more swaps. In the worst case scenario, while bubble sort performs $$n*(n-1)$$ swaps, selection sort only performs $$n$$ swaps. Hence Selection sort fares better than bubble sort as there are more write operations performed in Bubble Sort than in Selection Sort.

In case of Selection Sort, number of comparison performed is **always** of the order of $$n^{2}$$  since comparision is performed on the remaining unsorted elements, while in case of Insertion Sort, number of comparision is $$n^2$$ **only**  in the worst case. The comparison is performed over the sorted elements. Hence Insertion sorts performs better than selection sort in average case and is equal to selection sort in worst case performance.

To prove this point, I created 10 random lists of positive integers. The size of the list ranged from 1,000 to 100,000 in the steps of 10,000. I then ran the three algorithms on each of the 10 list and measured the time taken to sort the list with these three algorithms. The plot validated the above point

![useful image](/assets/performance_of_sorting_algo.png)

We can see, bubble sort is the worst performer, followed by selection sort. Insertion sort is pretty fast when compared with these two algorithms.

