---
description: Solving problems in a systematic way
---

# Problem Solving

## 1. Clarification of problem, Assumptions(Clarification & Assumption)

* make the requirements&#x20;
* use cases as clear as possible

## 2. Problem Abstraction(High Level)

* identify the key point of the problem, and discrete math model
* abstract the key problem into a well-defined one（找到它实际对应的问题，注意condition）
* with very strict environment requirement
  * data type? data quantitative(positive/ negative)? data scaling (sparse?)
  * unique solution?



## 3. Algorithmic Design(Mid Level + TC\&SC)

* Solve the well-defined problem as efficiently as you can
  * Proposing multiple solutions is very necessary
  * Complexity analysis



## How to ?

* starting from the concrete example to abstract example(题目本身的提炼，找规律)
* There are only a few ways to start the algorithmic design:
  * **Greedy(BFS & maintain a global candidate)**
    * start from the smallest one, and find the next smallest one for k steps
      * so we can utilize the peek() or poll() for each step
      * **Best First Search**
    * global candidate
      * always maintain the k candidates and do necessary updates
    * etc...
  * **Brute Force (DFS all paths)**
    * find all possible things
      * 找好了分解的基准
      * 逻辑解耦
    * find possible optimizations
      * **remove the unnecessary computation**
      * **remove the repeated computation**
  * **Divide & Conquer (pure recursion & real div)**
    * solving problems by using subproblems result
      * binary search?
      * kth smallest in two sorted array
      * quickselect
      * kth smallest in BST

## 4. Practical Concern

* Identify the real-world environment and requirement
* **multiple solutions, necessary modifications**
* **trade-off analysis**

