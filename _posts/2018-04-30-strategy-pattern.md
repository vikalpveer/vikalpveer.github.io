---
layout: post
title: "Strategy Design Patterm"
date: "2018-04-30"
slug: "strategy-design-pattern"
description: "Understanding Strategy Design Pattern"
category: 
  -Design Pattern
# tags will also be used as html meta keywords.
tags:
  - Design_Pattern
  - Coding
show_meta: true
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

Strategy Pattern is a behavioral software design pattern that allows runtime selection of a behavior. This means that depending on the context (object), a suitable behavior (strategy) can be called.
<!--more-->
 Let's say I have a client who want to implement array rotation on a sorted array. I write a **class Solution** which  do some array manipulationsvia API **doRotation**. I also provide an API **doSort** to my client . *doSort* sorts the given vector of integer according to bubble sort algorithm. 
My client say he wants more flexibility with the sorting algo and he should be allowed to choose between **Bubble Sort**, **QuickSort** and **Merge Sort** algorithm. I will say OK and while I am thinking about something like adding some if/else clause in my *doSort()* method, client say, in future he would like to have few more sort algorithms to be added as well.

On same day, I get another call from a different client who wants various sort function APIs available to him. Now I want to work efficiently and want to leverage the *doSort* logic implmented in *Solution* class and design a way so that I can do maxium code reuse and satisfy the requirement of both clients. Strategy Pattern will come handy here.


{% highlight c++ %}
// I will define an interface Sort_Algo which would provide an 
// Interface to implement various sort algo and provide scope to
// add more algos in future.

class Sort_Algo {
    // Array to be sorted
    vector<int> A;
    public:
        // Constructor
        Sort_Algo(vector<int> a) : A(a) {}
        // This is the virtual function to implement
        // actual sort logic
        virtual void sort() = 0;
};

//As I learn new algo, I will inherit Sort_Algo class and implement the sort function.

class BubbleSort::public Sort_Algo() {
    public:
        void sort() {
            //Sort A here according to bubble sort logic
        }
};
class QuickSort::public Sort_Algo() {
    public:
        void sort() {
            //Sort A here according to QuickSort logic
        }
};

class MergeSort::public Sort_Algo() {
    public:
        void sort() {
            //Sort A here according to MergeSort logic
        }
};
// When I learn more algo, I will add it's imeplentation here.
{% endhighlight %}

Now you can see, I can give this class straightaway to my second client so that he can sort A as he likes. I can add more algorithms as I learn. Clean stuff so far.
For my first client, I have to implement a *class Solution* which also has to roate the array after sorting the array. Since I already have my Sort_Algo interface ready, my *class Solution* can compose *Sort_Algo* class within Solution and provide scope for dynamically change the sorting behavior. Below code will make sense of this.

{% highlight c++ %}

class Solution {
    // Vector in question
    vector<int> A;
    
    // Instead of actually implementing our sort here, we will 
    // use the Sort_Algo interface.
    Sort_Algo *algo;
    public:
        Solution(vector<int> a) : A(a) {
            // set default algo to BubbleSort
            algo = new BubbleSort(A);
        }
        void doRotation() {
            // Do some mainpulation on array as asked by client
        }
       
        // We expose this API allowing our client to set the algo as they want
        void setSort(Sort_Algo *a) {
            algo = a;
        } 
        void doSort() {
            // Appropirate Algo of sort would be called.
            algo->sort();
        }
};

// Client program

int main() {
    vector<int> a = {1,2,3};
    Sort S(a);
    
    S.doSort(); // Default bubblesort would be called.

    // I want to sort using Quicksort so I set algo in my sort class to Quicksort
    Sort_Algo *a = new QuickSort();

    s.setAlgo(a);
    s.doSort(); // This time A would be sorted using quicksort.

   // I am not satisfied with quicksort. Want to do merge sort
    a = new MergeSort();
    s.setAlgo(a);
    s.doSort();

    s.doRotation() // other stuffs you want to do on A.

}
{% endhighlight %}


 <div class="mermaid">
  graph LR
      A --- B
      B-->C[fa:fa-ban forbidden]
      B-->D(fa:fa-spinner);
  </div>
