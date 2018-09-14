---
layout: post
title: "Largest Sum Subarray - Linear Time approach"
date: "2018-09-13"
slug: "largest-sum-subarray"
description: "Largest Sum Subarray : Find subarray with largest sum in linear time complexity"
category:
  - Algorithm
# tags will also be used as html meta keywords.
tags:
  - Algorithm
  - Greedy, Array
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

**Problem :** Given an array of positive and negetive integers, find the subarray with the largest sum and return this sum in Linear Time.

<!--more-->

Suppose our array only had positive integers. Then subarray with the largest integer is the whole array itself !

However, because the problem statements states that the array can have $$+^{ve}$$ and $$-^{ve}$$ integers, we have to consider each possible subarrays, calculate its sum and bookeep the maxium sum. When all subarrays has been considered, return the maxium sum. This is a *naive* approach to solve this problem.

The time complexity of this approach is $$\theta(n^{2})$$. Can we do better ?

Indeed we can solve this problem in linear time complexity i.e $$\theta(n)$$ using a **Greedy Approach**

**Linear time approach**

We use two variables *curr_sum* and *max_sum* to store the sum of the current subarray and the maximum sum found so far. We  initialize these two variables  with the first element of the given array.

The idea of linear time is simple. We iterate through the remaining elements of the array and at each iteration we add element at the current index to the *curr_sum*.  Additionaly check if the value of the new *curr_sum* is less than the current element, then update *curr_sum* to current element becuase starting from the current element gives you higher sum. In each iteration, update *max_sum* if *curr_sum* is greater than the *max_sum* found so far.

At the end of the iteration, return *max_sum*. Following graphics explains the logic. Blue cells indicate the current subarray. 

{% include_relative img/largest_sum_subarray.svg %}

The time complexity of this algorithm is  $$\mathbf{\theta(n)}$$ as we iterate through the array only once.

Following is the python and c++ implementaion of the above logic.



### Python Implementation

```python
def maxSubArray(nums):
        curr_sum = nums[0]
        max_sum = nums[0]
        
        for i in range(1,len(nums)):
            curr_sum += nums[i]
            if curr_sum < nums[i]:
                curr_sum = nums[i]
            max_sum = max(max_sum, curr_sum)
            
        return max_sum

```



### C++ Implementation

```c++
	int maxSubArray(vector<int> &nums) {
        
        int max_sum = nums[0];
        int curr_sum = nums[0];
        for(int i = 1; i < nums.size(); i++) {
            curr_sum = curr_sum + nums[i];
            if(curr_sum < nums[i]) {
                curr_sum = nums[i];
            }
            
            max_sum = max(max_sum, curr_sum);
        }
        
        return max_sum;
    }
```
