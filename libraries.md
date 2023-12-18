Default:math

zip
enumerate

## Built-in Functions 
[W3Schools Built-in Functions](https://www.w3schools.com/python/python_ref_functions.asp)

### `enumerate()`
The enumerate() function is a built-in function that returns an enumerate object. This lets you get the index of an element while iterating over a list.

The basic syntax is is enumerate(sequence, start=0)

The output object includes a counter like so: (0, thing[0]), (1, thing[1]), (2, thing[2]),

As input it takes a sequence like a list, tuple or iterator. The start parameter is optional.
If the start parameter is set to one, counting will start from one instead of zero

```python
letters = ['a','b','c']
for i, letter in enumerate(letters):
    print('letters', i, '=', letter)
# output: letters 0 = 'a'
#         letters 1 = 'b'
#         letters 2 = 'c'
    print(i,letter)
# output: 0  'a'
#         1  'b'
#         2  'c'

```
```python
letters = ['a','b','c']
y = enumerate(letters)
print(next(y)) # (0,'a')
print(list(y)) # [(0, 'a'), (1, 'b'), (2, 'c')]

* **Enumerating a string**
```python
word = "Apple"
for i,letter in enumerate(word):
  print(i,letter)
# 0 A
# 1 p
# 2 p
# 3 l
# 4 e
```


### Itertools.zip_longest() 

This iterator falls under the category of Terminating Iterators. It prints the values of iterables alternatively in sequence. If one of the iterables is printed fully, the remaining values are filled by the values assigned to fillvalue parameter.

```python
from itertools import zip_longest   
x =[1, 2, 3, 4, 5, 6, 7]   
y =[8, 9, 10]   
z = list(zip_longest(x, y))   
print(z)  # [(1, 8), (2, 9), (3, 10), (4, None), (5, None), (6, None), (7, None)]
```

### zip()

The zip() function returns a zip object, which is an iterator of tuples where the first item in each passed iterator is paired together, and then the second item in each passed iterator are paired together etc.

If the passed iterables have different lengths, the iterable with the least items decides the length of the new iterator.


```python
a = "ab"
b = "xyz"

x = zip(a, b)

print(tuple(x))
# (('a', 'x'), ('b', 'y'))
```

1768. Merge strings alternately

You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return the merged string.

Example 1:

Input: word1 = "abc", word2 = "pqr"  
Output: "apbqcr"  
Explanation: The merged string will be merged as so:  
word1:  a   b   c  
word2:    p   q   r  
merged: a p b q c r  

Example 2:

Input: word1 = "ab", word2 = "pqrs"  
Output: "apbqrs"  
Explanation: Notice that as word2 is longer, "rs" is appended to the end.  
word1:  a   b  
word2:    p   q   r   s  
merged: a p b q   r   s  

Example 3:

Input: word1 = "abcd", word2 = "pq"  
Output: "apbqcd"  
Explanation: Notice that as word1 is longer, "cd" is appended to the end.  
word1:  a   b   c   d  
word2:    p   q   
merged: a p b q c   d  


Solution using zip:
```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        result = "".join(a + b for a, b in zip(word1, word2))
        result += word1[len(word2):] + word2[len(word1):]
        return result
```
Using zip_longest:

```python
from itertools import zip_longest
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        result1 = zip_longest(word1, word2, fillvalue="")
        result = "".join(a+b for a,b in result1)
        return result   

```




