---
layout: post
title: "Common STLs or Data Structures for Coding Interview"
date: "2018-05-08"
slug: "Important-STL-DataStructure"
description: "Importan STLs and Data Structures one should know for Coding Interview"
category: 
  -Algorithm, Data Structure, Interview
# tags will also be used as html meta keywords.
tags:
  - Algorithm
  - Coding
  - Data Structure
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
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
videocredit: tedtalks
---
In this post I am consolidating important STLs and Data Structure Collection C++ and python provide which one can use to ace the coding interview. It is sometime handy to know these data structures and their complexity. 
<!--more-->

For example, if an interview solution requires you to use a sorted string, it is better to use inbuilt sort function rather than implementing your own sort logic.

* TOC
{:toc}

### Sort
If a part of your solution requires you to sort a string, or a container, c++ provides std::sort function.Average time complexity of sort function is $$O(nlogn) $$
C++ Syntax

`std::sort(start iterator, end iterator)`

Ex:
{% highlight c++ %}
#include <iostream>
#include <algorithm>
#include <vector>

main() {
    int t_arr[] = {10,5,15,13,12,8};
    std::vector<int> c(t_arr, t_arr + 6);
    std::sort(c.begin(), c.end());
    int i = 0;
    while(i < c.size()) {
        std::cout << c[i] << " ";
        i++;
    }
    std::cout << "\n";
}
Output:
5 8 10 12 13 15
{% endhighlight %}

### List
List in C++ is implemented as a doubly linked list. Hence it has $$O(1)$$ insert, delete time. Following are the important methods which can be  useful for programming.

1. **front and back** : Directly accessing first and last element of the list.
2. **begin and end** : iterator for the first and *past last element* of the list. 
3. **push_front and push_back** : insert an element at the start or at the end of the list respectively.
4. **pop_front and pop_back** : remove element from the start of the list or from the end of the list respectively and effectively decreases the size of the list by 1. (returns none).
5. **erase** : remove the given iterator position. Can also be used to erase a range.
6. **size** : returns size of the list.
7. **sort** : sorts the list. Helpful when you have to sort the list as part of the solution. See Sort function above.

*PS: end() is past the last element hence would not give the access to the last element*

### Map / Unordered_Map
Major difference between ordered and unordered map is that unordered map can give $$O(1)$$ get value. Following are the important methods which can be useful for Coding your solution.

1. **begin and end** : iterator for the first and *past last element* of the list. 
2. **find** : find a given key in the map.
3. **erase** : remove the given iterator position. Can also be used to erase a range. You can remove a given key as well.

### Priority Queue
Well implementing a priority queue itself can be an interview question, but what if a logic you are thinking for a given problem requires priority queue or (max/min heap) ? Ofcourse you can implement your own heap algorithm but when you are constraint for time, use Standard **Priority Queue** to solve the problem. You can let your interviewer know that you are using language provided heap to solve this problem and if asked by interviewer, implement it later.

Here is the library functions provided by the c++ priority queue.
{% highlight c++ %}
#include <iostream>
#include <queue>
main() {

    std::priority_queue <int> q;
    q.push(5);
    q.push(10);
    q.push(4);
    q.push(20);
    q.push(12);

    while(!q.empty()) {
        std::cout << q.top() << " ";
        q.pop();
    }
    std::cout << "\n";
}

Output would be : 20 12 10 5 4
{% endhighlight %}





