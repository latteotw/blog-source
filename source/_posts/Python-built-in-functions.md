---
title: Python built-in functions
date: 2020-02-06 11:31:13
tags:
  - Python-Built-In-Functions
categories:
- [Python]
gitalk:
  id: /blog/python-built-in-functions/
---
* **Range**

  From [Python official document](https://docs.python.org/3/library/functions.html#func-range):
  >class range(stop)
  >
  >class range(start, stop[, step])
  >
  >Rather than being a function, range is actually an immutable sequence type, as documented in Ranges and Sequence Types >— list, tuple, range.

  Range is a little bit different than all other built-in functions. It's essential a data type that's built-in in Python. More specifically, it shares the same feature of list and tuple - it's sequential. Let's introduce some features and usage of range.

    * Start is inclusive and stop is exclusive
      ```python
      for i in range(1, 3, 1):
          print(i)
      ```

      This will print:
      ```
      1
      2
      ```
      <!--more-->
    * You can ignore step parameter. When step is ignored, it defaults to ```1```
      ```python
      for i in range(1, 3):
          print(i)
      ```

      This will print the same as above

    * You can ignore both start and step. When start is ignored, it defaults to ```0```
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

    There are more advanced usage of range is discussed at [this post](https://pynative.com/python-range-function/).

* **reversed()**

  Python3 has reversed() as a built-in function which takes a ```seq``` as input. According to [Python's official documentation](https://docs.python.org/3/library/functions.html#reversed)
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
