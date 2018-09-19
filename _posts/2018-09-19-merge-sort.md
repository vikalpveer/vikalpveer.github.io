---
layout: post
title: "Merge Sort Algorithm - Implementation and Analysis"
date: "2018-09-19"
slug: "merge-sort"
description: "Merge Sort is a **Divide and Conquer** sorting algorithm with a runtime complexity of $$\theta(nlogn)$$"
category:
  - Algorithm
# tags will also be used as html meta keywords.
tags:
  - Algorithm
  - Sorting
  - Divide and Conquer
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
Merge Sort is a **Divide and Conquer** sorting algorithm with a runtime complexity of $$\theta(nlogn)$$
<!--more-->
The simplest implementation of the merge sort algorithm requires an auxilary space of the order of $$O(n)$$ . In this post, I will present this simplest implementation of *mergesort* algorithm along with another attempt to  reduce the space complexity to the $$O(1)$$ by implementing **in-Place** merging. I will also show how both these implementation of merge sort compares with insertion sort which is $$O(n^{2})$$algorithm. 

The idea of merge sort is based on Divide and Conquer Paradigm. We first recursively divide the array into subarrays until no more "Division" or "Partitioning" is possible. We then start merging the partitions in a **Bottom-Up** approach. After each merging, the merged partitions are sorted.  

![Merge Sort Algorithm](/assets/Merge_sort_algorithm_diagram.svg)

## Python Implementation with $$O(n)$$ Space Complexity.  

```python
    def merge_sort(self, data, start, end):
        if start == end:
            return
        
        mid = int((start + end)/2)
        
        # Divide or partitioning Stage
        # Recursive call 
        self.merge_sort(start,mid)
        self.merge_sort(mid+1, end)
        
        # check condition if the two halves are already sorted
        if data[mid] <= data[mid+1]:
            return
        
        # Take two auxillary arrays left and right
        # for the two partitions in the current
        # recurssion and store values from original
        # unsorted array.
        
        left = data[start: mid+1]
        right = data[mid+1: end+1]

        left.append(9999999)
        right.append(9999999)
        
        l = 0
        r = 0
        
        # MERGING STAGE
        # --------------
        # Iterate through left and right aux array
        # and update original array .after this iteration, 
        # the chunck from start to end
        # in the original array is sorted.
        
        for i in range(start, end+1):
            if left[l] <= right[r]:
                data[i] = left[l]
                l += 1
            else:
                data[i] = right[r]
                r += 1
```



## Python Implementation with In  Place merging. $$O(1)$$ space complexity.

```python
    def InPlace_merge_sort(self, data, start, end):
        if start == end:
            return
        
        mid = int((start + end) / 2)
        
        # Divide or partitioning Stage
        # Recursive call 
        self.InPlace_merge_sort(start, mid)
        self.InPlace_merge_sort(mid+1, end)

        # check condition if the two halves are already sorted
        if data[mid] <= data[mid+1]:
            return
                
        l = start
        r = mid+1
        
        # Merging Stage
        # -------------
        # As long as element at 'l' is less than element at 'r'
        # continue.
        # else : 
        # All the remaining element in the left are greater 
        # than element at 'r' so shift the remaining array   
        # chunck in the left by 1 space
        # and copy the original element at 'r'
        # to the index at 'l'.
        
        while l <= mid and r <= end:
            if data[l] <= data[r]:
                l += 1
            else:
                temp = data[r]
                data[l+1:r+1] = data[l:r]
                data[l] = temp
                # everything needs to increment here.
                l += 1
                r += 1
                mid +=1
```



## comparing merge sort with insertion sort graphically

From the graph we can see that merge sort is significantly faster than insertion sort algorithm. This is due to the fact that insertion sort grows logarithamically which insertion sort grows quadratically. 


![Plot of Merge Sort with Insertion Sort](/assets/comparison-of-merge-sort-with-insertion-sort.png)
![Plot of Inplace Merge Sort with Insertion Sort](/assets/comparison-of-inplace-merge-sort-with-insertion-sort.png)
