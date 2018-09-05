---
layout: post
title: "Selection Sort Algorithm - Implementation and Analysis"
date: "2018-09-05"
slug: "selection-sort"
description: "Selection Sort is a simple in-place comparison based sorting Algorithm"
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

Selection Sort is a in-place sorting algorithm. The algorithm works by partitioning the given list such that elements left to the current index are sorted while elements on the right are unsorted. Algorithm compares each elements to the right to find the 
index of the minimum element less than the value at the current index. If such an index is found, the values at the two indexes are swapped and procedure is repeated for the next index.

<!--more-->

The algorithm requires two loops, the outer loop runs through each index of the array and is used as current index while inner loop runs though all the indexes to the right of the current index to find the index of the minimum element less than the value at the current
index. At the end of the inner loop is such an index is found, the values at the two indexes are swapped.

{% include_relative img/selection_sort.svg %}

Following is a python and C++ implementation of the Selection Sort algorithm:

## Python Implementation

{% highlight python %}
def sort(self, data):
    print("Sorting using selection sort")
    
    # To keep tracks of number of swaps
    num_swap = 0
    for i in range(len(data)):
        min_idx = i
        for j in range(i+1, len(data)):
            if(data[min_idx] > data[j]):
                min_idx = j
        if(min_idx != i):
            data[i], data[min_idx] = data[min_idx], data[i]
            num_pass = num_pass + 1
    print("Number of pass made %d" %num_pass)
{% endhighlight %}

## C++ Implementation

{% highlight c++ %}
void sortIntegers(vector<int> &A) {
    // Size of the vector
    int len = A.size();
        
    // Outer loop, for each index
    for(int i = 0; i < len; i++) {
          
        // Keep track of min element in 
        // right which is less than current element 
        int min_idx = i;
            
        // Inner loop runs though all elements 
        //right of current index
        for(int j = i + 1; j < len; j++) {
                
            // If smaller element is found, update min_idx 
            if(A[min_idx] > A[j] ) {
                min_idx = j;
            }
        }
            
        //If there exist an index in the right whose value is 
        // less than the current value, swap it.
        if(min_idx != i) {
            swap(A[i], A[min_idx]);
        }
    }
}
{% endhighlight %}

## Analysis of the algorithm

If $$n$$ is the length of the array, outer loop runs for n times and for each outer loop pass, algorithm runs for remaining element on the left side in the inner loop. Hence complexity of this algorithm is $$\Theta (n^{2})$$

One thing to note is that if array is already sorted, number of swaps in this case would be 0 while if array is in a descending order, there would be $$ n -1$$ swaps. Hence number of swaps required ranges from $$ 0 \ to\ n-1$$.

