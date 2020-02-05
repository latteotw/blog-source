---
title: Python List
date: 2020-02-04 15:47:42
tags:
  - Python-List
categories:
- [Python, List]
gitalk:
  id: /blog/python-list/
---
* **List Concatenation**

  There are two ways two concatenate a list with another. One is to use ```+``` to concatenate a list. Another way is to use ```extend()``` function to concatenate

  ```python
  # Use + to concatenation a list
  A = ['a', 'p', 'p', 'l', 'e']
  B = ['b', 'a', 'n', 'a', 'n', 'a']
  C = A + B
  print(C) # ['a', 'p', 'p', 'l', 'e', 'b', 'a', 'n', 'a', 'n', 'a']

  # Use extend() function to concatenate
  A.extend(B)
  print(A) # ['a', 'p', 'p', 'l', 'e', 'b', 'a', 'n', 'a', 'n', 'a']
  ```

  <!--more-->
  We can easily note that ```+``` creates a new list C which is the result of ```A + B```

  At the meanwhile, ```extend``` concatenate list B to original list of A. This means that no new list is created. It modifies list A in-place. This operation will usually save some space but we lost the track of A unless you ***copy*** the original elements of A into another list ahead of time. For how to copy a list, please see next section.

* **List Copy**

  To continue with the previous example, we can copy the list before we extend it so that we don't lose the track of the original list if we want.

  Before we go into the actual syntax, let's see the following example:

  ```python
  A = ['a', 'p', 'p', 'l', 'e']
  B = ['b', 'a', 'n', 'a', 'n', 'a']
  C = A
  D = A.copy()
  A.extend(B)
  ```

  In this case, what is the result of ```print(C)```?

  Also, What's the result of ```print(D)```?

  ```
  >>> print(A)
  ['a', 'p', 'p', 'l', 'e', 'b', 'a', 'n', 'a', 'n', 'a']
  >>> print(C)
  ['a', 'p', 'p', 'l', 'e', 'b', 'a', 'n', 'a', 'n', 'a']
  >>> print(D)
  ['a', 'p', 'p', 'l', 'e']
  ```

  Why?

  Let's see some more results first:
  ```
  >>> print(A.__str__)
  <method-wrapper '__str__' of list object at 0x103aa2588>
  >>> print(C.__str__)
  <method-wrapper '__str__' of list object at 0x103aa2588>
  >>> print(D.__str__)
  <method-wrapper '__str__' of list object at 0x103aa2688>
  >>> A == D
  False
  >>> A == C
  True
  ```

  What does this mean? ```print(A.__str__)``` function prints out the object description of A. ```0x103aa2588``` is the object address in memory.

  Here we can see that A and C has the same address in memory and D has a different address in memory. ```A == C``` equals ```true``` and ```A == D``` equals ```false``` also verify this statement.

  In order to know why we got this behavior, we have to look at how C and D is initialized.

  We had ```C = A``` and ```D = A.copy()```. The difference then became obvious:

  Statement like ```C = A``` did a shallow copy which copy the object of ```A``` to variable ```C``` so that ```A``` and ```C``` refer to the same address in memory.

  At the same time, ```D = A.copy()``` actually creates a new array ```D``` and we copied the actual item in ```A``` to ```D``` instead of simply refers the object of ```A``` to ```D```.

  It more or less similar to the following process:
  ```python
  D = []
  for item in A: D.append(item)
  ```
