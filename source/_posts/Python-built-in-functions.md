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
