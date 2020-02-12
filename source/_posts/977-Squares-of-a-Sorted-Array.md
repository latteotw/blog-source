---
title: 977. Squares of a Sorted Array
date: 2020-02-07 16:16:49
tags:
  - Array
  - Easy
  - Python-List
  - Two Pointers
categories:
  - Array
gitalk:
id: /blog/977/
---
https://leetcode.com/problems/squares-of-a-sorted-array/

# Problem Statement
>Given an array of integers ```A``` sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decrMeasing order.

> **Example 1:**
>
> Input: [-4,-1,0,3,10]
>
> Output: [0,1,9,16,100]

>**Example 2:**
>
> Input: [-7,-3,2,3,11]
>
> Output: [4,9,9,49,121]

# Problem Analysis
The input of this problem is an 1-D array. Also please notice that the input array is ***sorted*** and ***non-decreasing***. Usually when you see an input is sorted, you will always use this nature to resolve the problem. Also we are required to return the result in a sorted non-decreasing order. Since we are required to return a sorted result, I started to wonder whether the time complexity is O(N * lgN) since this is usually the minimal time complexity of algorithms that involve sorting. However, the nature of input array being sorted might also help us to improve the time complexity as well. Let's think about this problem with all these questions in mind.

# Thinking Process
We are given a sorted array A as input. We have to find the square of each elements in A and return the result of such an array in a sorted order. If all the elements in A are greater or equal to 0, we can just simply square every element and return the result. This will bring us the O(N) solution.

However, the exception is that the input list is not guaranteed to be positive. There could be negative numbers. Some negative numbers could have higher integer than some positive numbers. If we simply keep the original order of the input array and square every number up, then as the last step, sort the array and return it, we will get a O(N * lgN) time complexity answer. Let's see how that's implemented.

# First Solution
```python
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        for i in range(len(A)):
            A[i] *= A[i]
        return sorted(A)
```
or to be more pythonic (with worse space complexity):
```python
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        return sorted([i * i for i in A])
```
<!-- more -->
# Improvements
Before talking about the improvements, let's analyze the time complexity of the existing solutions.

The above two solutions both have ```O(N * lgN)``` time complexity where N is the length of the input array ```A``` because at the worst case, the sorting algorithm requires ```O(N * lgN)``` time complexity.

The space complexity for the first solution is ```O(1)``` since we modify and sort the original list in-place.

The space complexity for the pythonic one-liner is ```O(N)``` since we have to create a new list as the returned list.

Is there anyway to do it in linear time? The above two solutions didn't really use the nature of the input array being sorted. If the input array is not sorted, the above two solutions will yield the exactly same space and time complexity. Let's think about how can we find the maximum squared number by utilizing the input array sorted nature.

With the input array sorted, the largest squared number is either at the left-most or right-most of the list depends on whichever's absolute value is larger. Once we find the largest squared number of the current list, we append it to our answer list. Now, since the number is already used, we will only consider the remaining elements in the array. Depend on where we get the first element, we either move one step to the left or one step to the right. We repeat this process every time with a smaller sub-problem.

How do we keep track of the left and right position? We make two pointers - one pointer starts at the left of the array and another one starts at the end of the array. This is called **two pointer strategy**. At each iteration, we either pick one element from the position of the left pointer and move our left pointer one step to the right or we pick one element from the position of the right pointer and move our right pointer one step to the left.

When do we stop? We stop when the two pointer overlaps with each other. When two pointers overlap, we know we have already iterated every element in the array.

After iterating every list item, we get a new list with squared value of each element in the original list in a non-increasing order. However, we are required to return the answer as non-decreasing order so can just simply reverse the list.

```python
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        # We initialize the position of the left and start pointer.
        left, right = 0, len(A)-1
        ans = [] # Construct an empty list as the return value to hold our answer.
        while left <= right: # Set our loop terminate condition.
            if abs(A[left]) >= abs(A[right]):
                ans.append(A[left]**2)
                left += 1 # Move left pointer one step to the right.
            else:
                ans.append(A[right]**2)
                right -= 1 # Move right pointer one step to the left.
        return ans[::-1]
```

# Answer Analysis
> Time complexity: ```O(N)``` where N is the length of the input matrix.
>
> Space complexity: ```O(N)``` where N is the length of the input matrix.

This time complexity is faster than ```O(N * lgN)``` answer. The reason we can reach this linear time complexity is because we used the nature of the input array being sorted so we don't have to sort our answer again.

# Takeaways
1. Ways to sort a list in python:
    * list.sort() method
    List class comes with a class method called sort(). This algorithm sorts the list in-place. The time complexity is O(N * lgN). When we talk about sorting, I will dive deeper into the specific sorting algorithm that python uses.

    ```
    >>> a = [3,1,2]
    >>> a.sort()
    >>> a
    [1, 2, 3]
    ```

    * built-in sorted() function
    Python built-in functions also have a method to sort a iterable. This function is called ```sorted()```. It will return a sorted result of the input.
    ```
    >>> a = [3,1,2]
    >>> b = sorted(a)
    >>> b
    [1, 2, 3]
    ```

  2. Please take a look at [this blog](https://latteotw.github.io/2020/02/11/Two-pointers/) for ```two pointers``` techniques.
