---
title: 832. Flipping an Image
date: 2020-02-07 11:37:50
tags:
  - Array
  - Easy
  - Python-List
categories:
  - Array
gitalk:
  id: /blog/832/
---
https://leetcode.com/problems/flipping-an-image/

# Problem Statement
>Given a binary matrix A, we want to flip the image horizontally, then invert it, and return the resulting image.
>
>To flip an image horizontally means that each row of the image is reversed.  For example, flipping [1, 1, 0] >horizontally results in [0, 1, 1].
>
>To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting [0, 1, 1] >results in [1, 0, 0].

> **Example 1:**
>
>Input: [[1, 1, 0], [1, 0, 1], [0, 0, 0]]
>
>Output: [[1, 0, 0], [0, 1, 0], [1, 1, 1]]
>
>Explanation: First reverse each row: [[0, 1, 1], [1, 0, 1], [0, 0, 0]].
>
>Then, invert the image: [[1, 0, 0], [0, 1, 0], [1, 1, 1]]

>**Example 2:**
>
>Input: [[1, 1, 0, 0], [1, 0, 0, 1], [0, 1, 1, 1], [1, 0, 1, 0]]
>
>Output: [[1, 1, 0, 0], [0, 1, 1, 0], [0, 0, 0, 1], [1, 0, 1, 0]]
>
>Explanation: First reverse each row: [[0, 0, 1, 1], [1, 0, 0, 1], [1, 1, 1, 0], [0, 1, 0, 1]].
>
>Then invert the image: [[1, 1, 0, 0], [0, 1, 1, 0], [0, 0, 0, 1], [1, 0, 1, 0]]

# Problem Analysis
The input is a matrix which means that we are dealing with a 2-D array. 2-D array in python can be implemented as 2-D list. 2-D list is a list of list. The inner list represents the elements in each row and the outer list represents all the rows. We are asked to do two things, one is to flip the matrix and also invert the value. We can quickly think this as a minimum ```O(M * N)``` time complexity algorithm, where M and N represents the dimension of the matrix, because we have to go through each elements in the list. Space complexity is unknown until we know how can we flip the matrix.

# Thinking Process
The steps are very obvious: flip and then invert. Let's think about it one by one.

How should we flip a list in python? There are couple ways to do it:

1. Use built-in function reversed()

2. Use List class method reverse()

3. Use List slicing [::-1]

We will talk about the differences between them in the takeaways section. We will just choose one to use.

After knowing how should we flip a single list, we should think about how should we flip the whole matrix. The answer is very obvious. Row by row.

We also have to invert each ```0``` to ```1``` and ```1``` to ```0```. This can be done by using ```1 - value```.

Now it's clear to us the we should iterate through each row of the matrix and flip them. At the same time, we should invert the values. Let's see what's the most intuitive solution:

# First Solution
```python
class Solution:
    def flipAndInvertImage(self, A: List[List[int]]) -> List[List[int]]:
        for row in A: # Iterate through each row in A
            row.reverse() # We flip each row
            for i in range(len(row)):
                row[i] = 1 - row[i] # Invert the value
        return A
```
<!-- more -->
# Improvements
The time complexity of this algorithm is what we desired: ```O(M * N)```. I couldn't think of faster ways to implement this algorithm. In regard of the space complexity, let's see what's the current one's. We used ```row.reverse()``` function to implement the flipping. What's the space complexity of this operation? It's ```O(N)```. We will talk about the details in later section. This yields ```O(M * N)``` space complexity. Actually, for all the methods that reverse the list, they are at least ```O(N)``` space complexity so there's no room to improve the space complexity either. The next way to improve this algorithm is to think about the syntax simplicity. There's a pythonic answer:

```python
class Solution:
    def flipAndInvertImage(self, A: List[List[int]]) -> List[List[int]]:
        return [[1 - i for i in row[::-1]] for row in A]
```

# Answer Analysis
The improved algorithm doesn't help with improving the time and space complexities.
> Time complexity: ```O(M * N)``` where M x N is the dimension of the input matrix.
>
> Space complexity: ```O(M * N)``` where M x N is the dimension of the input matrix.

# Takeaways
1. Reverse a list

    As we have talked earlier, there are couple of different ways to reverse a list. We will talk about them one by one.

    * Using built-in reversed() function

      Python3 has reversed() as a built-in function which takes a ```seq``` as input. According to [Python's official documentation](https://docs.python.org/3/library/functions.html#reversed):
      >seq must be an object which has a __reversed__() method or supports the sequence protocol (the __len__() method and the __getitem__() method with integer arguments starting at 0).

      One thing to notice is that reversed() return an iterator. To make the iterator a list, you have co explicitly cast it. For example:
      ```
      >>> a = [1, 2, 3]
      >>> b = reversed(a)
      >>> b
      <list_reverseiterator object at 0x1090762e8>
      >>> list(b)
      [3, 2, 1]
      ```
      It has O(N) time and space complexity.

    * Using List class method reverse()
      List class contains a class method called ```reverse()``` which modifies the object **in-place** to reverse it. Even though the list is modified in-place, it still requires O(N) time complexity because it requires additional extra memory during the reverse.

      Example:
      ```
      >>> a = [1, 2, 3]
      >>> a.reverse()
      >>> a
      [3, 2, 1]
      ```
      It has O(N) time and space complexity.

    * Using list slice
      List can also be reversed using slicing syntax such as a[::-1]. This doesn't modify the original list so you have to assign it to another variable. For example:

      ```
      >>> a = [1, 2, 3]
      >>> b = a[::-1]
      >>> b
      [3, 2, 1]
      >>> a
      [1, 2, 3]
      ```
      It has O(N) time and space complexity.

2. List comprehension

    I used list comprehension in the improved algorithm. List comprehension is a really useful and clean syntax to construct a list. For more details, please refer to this [official python documentation](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions).
