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
