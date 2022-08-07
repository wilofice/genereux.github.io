---
layout: post
title: Time complexity (estimating efficiency)
image:
  path:    /assets/img/posts/tutorials/time_complexity_2.png
comments: true
tags: [data structures, complexity]
---

In this article, we are going to see more detail about how to estimate the efficiency of an algorithm based on its time complexity

1. toc
{:toc}

## Phases

Phases are dominant parts of the algorithm. For instance, in the example below, the code has three phases. Each phase has its time complexity. 

~~~c++
// Phase one
for (int i = 1; i <= n; i++) {
    // code
}

// Phase two
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        // code
    }
}

// Phase three
for (int i = 1; i <= n; i++) {
    // code
}
~~~

If the algorithm consists of many phases, the total time complexity is the time complexity of the dominant phase. The dominant phase corresponds to the slowest part of the algorithm, the one that runs in the longest time. Indeed, it is usually the bottleneck of the code. 

In the example above, the code has three phases with time complexities O(n), O(n<sup>2</sup>), and O(n).
So the time complexity of the code is 0(n<sup>2</sup>) because it is the slowest one.

## Time complexity with multiple factors

Often the time complexity of an algorithm may depends on many constraints.
That can happen when the input size is multidimensional like a 2D or 3D array .
Or it may be because the algorithm depends on different inputs with different constraints. 
In that case, the time complexity is function of the independants variables that caracterize the input.
For instance, the following code has a time complexity of O(mn).
~~~c++
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
        // code
    }
}
~~~


The specific case of Recursion

The time complexity of a recursive function depends on the number of times the function is called and the time complexity of a single call. The total time complexity is the product of these values.

For example, consider the following function:
~~~c++
void f(int n) {
    if (n == -1) return;
    f(n-1);
}
~~~

The call f(n) required n function calls to compute the final result, and the time complexity of each call is O(1).
Thus, the total time complexity is O(n).


## Evaluating an algorithm efficiency

Evaluating a time complexity of an algorithm before implementing it in production code or a coding competition is an excellent way to check if it is sufficient enough to solve the problem while complying with the performance constraints. 
Modern computers today can perform hundreds of millions of operations in a seconds but they still have some limits. In a real time application, you may be running your code on a dataset of billion of users per minute. In that case, your code must be the fastest possible. 

For instance, let's assume that the time limit for a problem is one second and the input size is n = 10<sup>5</sup>; Let's suppose you have designed an algorithm of O(n<sup>2</sup>) time complexity. It will require about (10<sup>5</sup>)<sup>2</sup> = 10<sup>10</sup> operations. That means your solution will run in at least tens seconds. It is then two slow for solving the problem. 

But given the input size, we can try to guess the required time complexity of the algorithm that solves the problem. 

The table below indicates useful estimations assuming with we have a time limit of one second to solve the problem. 

| input size      |  maximum required time complexity |
| --------------- | ------------------------ |
| n <= 10         | O(n!)       |
| n <= 20          | O(2<sup>n</sup>)       |
| n <= 500          | O(n<sup>3</sup>)       |
| n <= 5000          | O(n<sup>2</sup>)       |
| n <= 10<sup>6</sup>          | O(nlogn) or O(n)   |
| n is large          | O(1) or O(logn)       |


Base on that table, you can guess that the algorithm that solves the problem is expected to have a time complexity of O(n) or O(nlogn).

This information is crucial because it reduces the field of possibilities of the algorithms that can solve the problem. It makes easier to design the efficient solution. 

However we must not forget that a time complexity is only an estimation of the algorithm efficiency because it hides the constant factors.  An algorithm that runs in O(n) time may perform 2n or 5n operations. It is a detail that has an important effect on the actual running time of the algorithm.

In the next article in this serie, we are going to work on a example of differents algorithms to solve a concrete programming problem.

























