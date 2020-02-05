---
title: 1304. Find N Unique Integers Sum up to Zero
date: 2020-02-03 18:20:48
tags:
  - Array
  - Easy
  - Python-List
categories:
  - Array
gitalk:
  id: /blog/1304/
---
https://leetcode.com/problems/find-n-unique-integers-sum-up-to-zero/
# Problem Statement
> Given an integer n, return ***any*** array containing n ***unique*** integers such that they add up to 0.



# Problem Analysis
We firstly note that the input is an integer **n** and output is an **array**. Furthermore, we find that the output is not unique, which means that we have to construct an output that meet the requirement of the problem and there could be multiple or even infinite number of correct answers to this problem. This is rarely seen in a coding interview.

Another important thing that we notice from the question statement is that elements we use in the answer must be unique, which means we cannot reuse any of the element.

# Thinking Process
Firstly we noticed that we need to construct an array that sums to 0. It's really natural to think about the following way of constructing the array:
> [-n, -n-1, -n-2, ..., -3, -2, -1, 0, 1, 2, 3, ..., n-2, n-1, n]

Since we need n elements in the array, which means we need n/2 elements on the positive side and n/2 on the negative side so that they can easily sum up to zero. The dealbreaker here is whether we need to include 0 in the array. On which circumstances do we need to include 0? When n is odd. Otherwise we don't need 0. With this thinking process, it's very easy to come up with the following naive solution:

# First Solution
```python
class Solution:
    def sumZero(self, n: int) -> List[int]:
        answer = [] # We construct an empty array to hold the result
        for i in range(1, (n//2) + 1):
            answer.extend([i, -i])
        if n % 2 != 0: answer.append(0) # We add 0 when n is odd
        return answer
```
<!-- more -->
# Improvements
Let's analyze the time complexity and space complexity of our first algorithm.
> Time complexity: O(N) because we need to iterate the loop for n/2 times.
>
> Space complexity: O(N) because our answer array has exactly n elements.

We won't be able to simplify the space complexity for sure because we anyway need to return an array with size n. Also, I don't think there are easy ways to improve the time complexity as well because how many elements need to be constructed is depend on the input integer n and we have already reached a linear algorithm. So my focus will be at improving the code itself.

What's the ugly part in our code? I guess the first thing I want to get rid of is the if statement. How can we get rid of it? Let's do some observations of the following constructions:

> n = 1, [0]
> n = 2, [-1, 1]
> n = 3, [-2, 0, 2]
> n = 4, [-3, -1, 1, 3]
> n = 5, [-4, -2, 0, 2, 4]

What's rule can we derive from it?

> The i-th element of the returning array = i * 2 - n + 1

Now with the derived rule, we can get the following improved algorithms:
```python
class Solution:
    def sumZero(self, n: int) -> List[int]:
        answer = []
        for i in range(n):
            answer.append(i * 2 - n + 1)
        return answer
```

To be more Pythonic:
```python
class Solution:
    def sumZero(self, n: int) -> List[int]:
        return [i * 2 - n + 1 for i in range(n)]
```

# Answer Analysis
The improved algorithm doesn't help with improving the time and space complexities.
> Time complexity: O(N)
>
> Space complexity: O(N)

# Takeaways
The main take aways for this problem will be about python.

1. Different ways to concatenate two lists

    ```python
    a = [1, 2, 3]
    b = [4, 5, 6]

    # Method 1: using +
    print(a + b) # [1, 2, 3, 4, 5, 6]

    # Method 2: using extend
    a.extend(b)
    print(a) # [1, 2, 3, 4, 5, 6]
    ```

    The difference between using + and extend is that + will create a new list while extend modifies the first list in-place. Extend will save some space for most use cases.

2. Python list comprehension

    Please refer to [this awesome post](https://www.programiz.com/python-programming/list-comprehension) for how to use python list comprehension

3. // and / for division operations

    Depend on which version of python you use, // and / works differently
    ```python
    # python3
    3 // 2 # = 1
    3 / 2 # = 1.5

    # python2
    3 // 2 # = 1
    3 / 2 # = 1
    3 / 2.0 # = 1.5
    ```
