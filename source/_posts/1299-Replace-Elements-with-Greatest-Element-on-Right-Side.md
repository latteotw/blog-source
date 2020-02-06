---
title: '1299. Replace Elements with Greatest Element on Right Side '
date: 2020-02-05 16:11:31
tags:
  - Array
  - Easy
  - Python-List
categories:
  - Array
gitalk:
  id: /blog/1299/
---
https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/

# Problem Statement
> Given an array ```arr```, replace every element in that array with the greatest element among the elements to its right, and replace the last element with -1. After doing so, return the array.

> **Example 1:**
>
>Input: arr = [17,18,5,4,6,1]
>
>Output: [18,6,6,6,1,-1]


# Problem Analysis
Our input for this problem is an array and we are required to replace **every** element in the array with another number. This means that we have to iterate through the array for at least once. This yields at least O(N) time complexity. We also noticed that the last element is always -1. What we have to return is the modified array or a new array. This means that if we can modify the array in-place, we could reach a O(1) space complexity.

# Thinking Process
The very intuitive solution is to start from the first element in the array and move to the right one by one. At each element, we find the maximum number on the right. However, it's easy to get the time complexity of this algorithm which will be O(N^2). This is way too slow.

The question to ask is why do we have to iterate through each element on the right of the current index? Because we have to find the current maximum on the right every time we move the index. Is there anyway for us to find the current maximum on the right without iterating through the sub-array to the right of the index? Yes, we can start from the last element of the array. Every time we move the index to the left by one, we have already known what's the maximum from the right-most point to the current index. This easily yields the following O(N) answer:

# First Solution
```python
class Solution:
    def replaceElements(self, arr: List[int]) -> List[int]:
        cur_max = -1 # We keep track of what's the current maximum number from the right-most point.
        # cur_max is initialized to -1 because the last element is -1.
        for i in range(len(arr)-1, -1, -1):
            arr[i], cur_max = cur_max, max(cur_max, arr[i])
        return arr
```
<!-- more -->
# Improvements
There's not much improvements to talk about because I think we have already reached the best time complexity and the best space complexity.

# Answer Analysis
The improved algorithm doesn't help with improving the time and space complexities.
> Time complexity: O(N)
>
> Space complexity: O(1) since we modified the input array in-place.

# Takeaways
1. Swap operation

    In most of other programming language, when you have to swap two elements, you have to do something like:
    ```python
    a = 1
    b = 2
    temp = a
    a = b
    b = temp
    ```
    This means that we usually need to find a temporary place holder for one of the elements that need to be swapped.
    Just think about the case when you have to swap the liquid in two glass bottles. How would you do it?

    With python, there's a syntax sugar where you can do something like:
    ```python
    a = 1
    b = 2
    a, b = b, a
    ```
    Every element of the left side of ```=``` are assigned with their corresponding value on the right side of ```=```

2. Usage of range()

    range() is a built-in function of python. The formal Python3 documentation has two prototypes for the built-in range function:

    > class range(stop)
    >
    > class range(start, stop[, step])

    Without specifying the step, the default step size is 1.
    Let's see the following examples:
    ```python
    for i in range(3):
        print(i)
    ```
    This will print:
    ```
    0
    1
    2
    ```

    ```python
    for i in range(5, 1, -2):
        print(i)
    ```

    This will print
    ```
    5
    3
    ```

    There are couple things to notice:

    * The range is **left inclusive** and **right exclusive**.

    * If you don't specify the start, it will always start from 0

    * If you don't specify the step, it will always default to 1
