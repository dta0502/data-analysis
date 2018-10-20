# Truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all()

转载于：[stackoverflow](https://stackoverflow.com/questions/36921951/truth-value-of-a-series-is-ambiguous-use-a-empty-a-bool-a-item-a-any-o)

## 问题描述

Having issue filtering my result dataframe with an `or` condition. I want my result df to extract all column `_var_` values that are above 0.25 and below -0.25. This logic below gives me an ambiguous truth value however it work when I split this filtering in two separate operations. What is happening here? not sure where to use the suggested `a.empty()`, `a.bool()`, `a.item()`, `a.any()` or `a.all()`.

```python
 result = result[(result['var']>0.25) or (result['var']<-0.25)]
```

## 解答

The `or` and `and` python statements require `truth-values`. For pandas these are considered ambiguous so you should use "bitwise" `|` (or) or `&` (and) operations:

```python
result = result[(result['var']>0.25) | (result['var']<-0.25)]
```

These are overloaded for these kind of datastructures to yield the element-wise `or` (or `and`).

---

Just to add some more explanation to this statement:

The exception is thrown when you want to get the `bool` of a `pandas.Series`:

```python
>>> import pandas as pd
>>> x = pd.Series([1])
>>> bool(x)
ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().
```

What you hit was a place where the operator implicitly converted the operands to `bool` (you used `or` but it also happens for `and`, `if` and `while`):

```python
>>> x or x
ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().
>>> x and x
ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().
>>> if x:
...     print('fun')
ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().
>>> while x:
...     print('fun')
ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().
```


Besides these 4 statements there are several python functions that hide some `bool` calls (like `any`,  `all`, `filter`, ...) these are normally not problematic with pandas.Series but for completeness I wanted to mention these.

---

In your case the exception isn't really helpful, because it doesn't mention the right alternatives. For `and` and `or` you can use (if you want element-wise comparisons):

- `numpy.logical_or`:

```python
>>> import numpy as np
>>> np.logical_or(x, y)
```

or simply the `|` operator:

```python
>>> x | y
```

- `numpy.logical_and`:

```python
>>> np.logical_and(x, y)
```

or simply the `&` operator:

```python
>>> x & y
```

If you're using the operators then make sure you set your parenthesis correctly because of the operator precedence.

There are several logical numpy functions which should work on `pandas.Series`.

---

The alternatives mentioned in the Exception are more suited if you encountered it when doing `if` or `while`. I'll shortly explain each of these:

- If you want to check if your Series is empty:

```python
>>> x = pd.Series([])
>>> x.empty
True
>>> x = pd.Series([1])
>>> x.empty
False
```

Python normally interprets the length of containers (like `list`, `tuple`, ...) as truth-value if it has no explicit boolean interpretation. So if you want the python-like check, you could do: `if x.size` or `if not x.empty` instead of `if x`.

- If your `Series` contains one and only one boolean value:

```python
>>> x = pd.Series([100])
>>> (x > 50).bool()
True
>>> (x < 50).bool()
False
```

- If you want to check the first and only item of your Series (like `.bool()` but works even for not boolean contents):

```python
>>> x = pd.Series([100])
>>> x.item()
100
```

- If you want to check if all or any item is not-zero, not-empty or not-False:

```python
>>> x = pd.Series([0, 1, 2])
>>> x.all()   # because one element is zero
False
>>> x.any()   # because one (or more) elements are non-zero
True
```


