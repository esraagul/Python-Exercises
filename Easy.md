# NOTES 
## Data Structures
Python has the following data types built-in by default, in these categories:

| **Category**    | **Types**                        |
|-----------------|-----------------------------------|
| **Text Type**   | str                               |
| **Numeric Types**| int, float, complex               |
| **Sequence Types** | list, tuple, range               |
| **Mapping Type** | dict                              |
| **Set Types**   | set, frozenset                     |
| **Boolean Type**| bool                              |
| **Binary Types**| bytes, bytearray, memoryview      |
| **None Type**   | NoneType.                         |

## 1) Array

* **Empty Array:** `[]`

* **Empty Array with Zeros:** `[]*n`

* **Initialization with Values (Mixed Types):**  
  ```python
  arr = [1, "eels"]
  ```
* **Accessing Items by Index (Negative Indexing for End of Array):**  
  ```python
  arr = [1, 2, 3, 4, 5, 6]
  arr[0]  # 1
  arr[-1] # 6
  ```
* **Supports Append and Insert Operations:**  
  ```python
  arr.append(8)    # appends 8 at the end of the array
  arr.insert(6, 7) # Inserts 7 at index 6 
  ```
* **Accessing Specific Locations in 2D Arrays:**
  ```python
  arr = [[1, 3], [2, 2], [3, 1]]
  value = arr[i][j]  # Accessing element at row i, column j
  arr[0][0] # To refer to 1 in [1, 3], you should use arr[0][0].
  ```
* **Generating a list of integers for given n**
  ```python
  #input: n = 3
  #output: [0,1,2]
  arr = [i for i in range(n)]
  #input: n = 3
  #output: [1,2,3]
  arr = [i+1 for i in range(n)]
  #input: n = 3
  #output: ["1","2","3"]
  arr = [str(i+1) for i in range(n)]
  ```
## 2) Dictionaries
A dictionary is a collection in Python that is ordered and changeable, and it does not allow duplicate members.
* **`Counter()` from collections**

### Example:

```python
romans = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
romans['I'] == 1

# Adding a new key-value pair to the dictionary
romans['E'] = 100000

# Getting keys and values from the dictionary
romans.keys()   # Returns a view object containing the keys of the dictionary as a list
romans.values() # Returns a view object displaying a list of all values in the dictionary

my_dict = {'a': 1, 'b': 1, 'c': 3}

Check if all values are smaller than 2
all_values_smaller_than_2 = all(value < 2 for value in my_dict.values())


dict.get(key, default) is a method that allows you to retrieve the value for a given key in a dictionary. 
If the key is present in the dictionary, dict.get() returns the corresponding value. 
If the key is not found, it returns the default value specified as the second argument.

my_dict.get('a') ---> 1

if count of the key is higher than 3 then return true
for value in count.values():
            if value >= 2:
                return True
```

## 3) Stack of characters

A stack is a linear data structure that stores items in a Last-In/First-Out manner, like books stacked on top of each other.

```python
stack = []
stack.append('a')  # Adds 'a' at the top of the stack
stack.append('b')
stack.append('c')
# The stack is 'cba' from top to bottom
stack.pop()  # Pops out the item at the top of the stack, which is 'c' here.
```

## 4) Strings

* `string.count():`  You can use the `count()` method in Python to count occurrences of a substring within a string.
```python
txt = "I love apples, apple are my favorite fruit"
x = txt.count("apple")
print(x) # 2
```

## 5) `bin()` Function

The `bin()` function returns the binary version of a specified integer. The result will always start with the prefix `0b`.

```python
bin(36)  # Outputs: 0b100100

# Store the binary representation in a variable
x = bin(36)
x = x[2::]  # Extract the binary part starting from the 2nd element onwards: 100100

```

## 6) Lists

Lists are used to store multiple items in a single variable.

**Difference between Array and List:**

Arrays can store elements only of the same type, whereas lists can store elements of different types.

**Example:**

```python
# List with different types of elements
my_list = ['esra', 28]

# Array with elements of the same type
my_array = [22, 28]

```

## 7) Set
Sets in Python are unordered collections of unique elements.

By their nature, duplicates aren't allowed. Therefore, converting a list into a set removes the duplicates.

Sets do not have append function, instead `set.add(element)` is used.  

## 8) Reversing an array
one way is to use `reversed()`:
``` python
array = [1, 2, 3, 4, 5]
reversed_array = list(reversed(array))
print(reversed_array)  
```
or build-in function `reverse()`:
```python
array = [1, 2, 3, 4, 5]
array.reverse()
print(array)  
```
## 9) `sorted()` Function

The `sorted()` function in Python is used to sort a sequence (such as a list) and return a new sorted list from the elements of any iterable. It takes an optional `key` argument, which can be a function or lambda expression used for custom sorting logic.

### Example 1:

```python
sorted(arr, key=lambda x: (bin(x).count('1'), x))
```
The `sorted()` function takes the input list arr and sorts its elements based on the key provided by the lambda function. Each element `x` in arr is transformed using the lambda function to obtain a tuple `(bin(x).count('1'), x)`. The sorting is done based on these tuples, first by the count of '1' bits and then by the actual values of x.

### Example 2:

```python
sorted_arr = sorted(boxTypes, key = lambda x: x[1], reverse= True) : descending order 
```
In this example, sorted_arr is sorted based on the second element of each tuple in boxTypes in descending order (reverse=True), demonstrating how the key argument can be used to customize sorting behavior.
********************************************************************************************************************************************************************

# QUESTIONS 
These are the questions from leetcode.

## 20) Valid Parentheses
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:
Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.

``` python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        mapping = {')':'(','}':'{',']':'['}
        for char in s:
            if char in mapping:
                top_element = stack.pop() if stack else '#'
                if mapping[char] != top_element:
                        return False  
            else:
                stack.append(char)
        return not stack
```

## 121) Best time to buy and sell stock
You are given an array prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

``` python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        
        ''' Brute force, too time consuming.
        n = len(prices)
        max_diff = 0
        for i in range(n):
            for j in range(i+1,n):
                diff = prices[j]-prices[i]
                if diff > max_diff:
                    max_diff = diff
        return max_diff
        '''
        n = len(prices)
        min_price = float('inf')
        max_profit = 0
        for i in range(n):
            if prices[i]< min_price:
                min_price = prices[i]
            else:
                if prices[i]- min_price > max_profit:
                    max_profit = prices[i]- min_price
        return max_profit
```

## 217) Contains Duplicate
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

``` python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        unique_set = set()
        for num in nums:
            if num in unique_set:
                return True
            unique_set.add(num)
        return False

```

## 1481) Least Number of Unique Integers after K Removals(medium)

Given an array of integers arr and an integer k. Find the least number of unique integers after removing exactly k elements.

Hint: An optimal strategy is to remove the numbers with the smallest count first.

This way is time complex since arr.count(a) iterates through all elements of arr, the overall time complexity of your code becomes O(n^2):

``` python
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        counts = {}
        for a in arr:
            counts[a] = arr.count(a)
        sorted_arr = sorted(arr, key = lambda x:(counts[x],x))
        return len(set(sorted_arr[k:]))
```

better approach is to use `Counter(arr)` from collections

```python
from collections import Counter
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        counts = Counter(arr)
        sorted_arr = sorted(arr, key = lambda x:(counts[x],x))
        return len(set(sorted_arr[k:]))
```
