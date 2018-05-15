---
layout: post
featured: true
title: "How to implement a stack"
date: "2018-04-29"
slug: "implement-stack"
description: "Implementing a stack in C++"
category: 
  - Data Structures
# tags will also be used as html meta keywords.
tags:
  - Data_Structures
  - Coding
show_meta: true
comments: true
mathjax: true
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
Stacks along with Queues are Data Structures which are often used to enforce strict order in which an element can be inserted or removed. A typical Stacks / Queues are usually implemented using an Array or a List. 

<!--more-->

### Implementation

Stacks enforce *Last In First Out* or **LIFO** ordering. This means that the first element inserted into the stack is the last element to be retrieved. Thus an elemment can be accessed only when all other elements inserted
after this elemenets have already been removed from the stack.

The method to insert an element into the stack is known as **PUSH** while the method to remove the element from the stack is known as **POP**. 
In order to implement the stack, we need to expose atleast these two methods to let our client program access the stacks. A stack may also expose a method to allow client to access the top most element from the stack without removing it from the stack. We will call this method **getTop**. Additionally the stack also need to throw an error if *getTop* or *pop* method is called on an empty stack. We can also impose a limit on the size of the stack. Hence if a stack is full, a *Push* operation should throw an error.

<div class="mermaid">
   graph TB
    c1-->a2
    subgraph one
    a1-->a2
    end
    subgraph two
    b1-->b2
    end
    subgraph three
    c1-->c2
    end 
</div>

With these design requirements, let's implement the stack. Following is the C++ implemenation.

### Code

{% highlight c++ %}
#include <iostream>
#include <list>

class Stack {
     std::list<int> S;
     int size;
     public:
         // Construction
         Stack(int s):size(s) { } 

         // method to push 'i' in the stack
         // Thus increasing the size of the stack
         // by 1.
         void push(int i) {
             if(S.size() == size) {
                  std::cout << "Stack is Full \n";
                  return;
             }   
             S.push_back(i);
         }   

         // Method to return top element from the stack
         int getTop() {
              if(!S.size()) {
                   std::cout << "Stack is empty \n";
                   return -1; 
              }   
              return S.back();
         }   

         // method to return top element from the stack
         // and remove it from the stack thus reducing
         // the size of stack by 1.
         int pop() {
             if(!S.size()) {
                  std::cout <<"Stack is empty \n";
                  return -1; 
             }   
             int i = S.back();
             S.pop_back();
             return i;
         }   
};

// Client

int main() {
     Stack s(3);

     s.getTop();
     s.push(6);
     std::cout << "Top Element is "<< s.getTop() << "\n";
     s.push(8);
     std::cout << "Top Element is "<< s.getTop() << "\n";
     s.push(4);
     std::cout << "Top Element is "<< s.getTop() << "\n";

     s.pop();
     std::cout << "Top Element is "<< s.getTop() << "\n";
     s.pop();
     s.pop();
     s.pop();
}

Stack is empty 
Top Element is 6
Top Element is 8
Top Element is 4
Top Element is 8
Stack is empty 

{% endhighlight %}


