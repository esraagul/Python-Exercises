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

### Methods:

* 1) join:  The join() method takes all items in an iterable and joins them into one string. A string must be specified as the separator.
     "".join(...): Joins the strings into a single string.
     


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
* **`index()`**

List.index() returns the index of the specified element in the list.
```python
animals = ['cat', 'dog', 'rabbit', 'horse']

# get the index of 'dog'
index = animals.index('dog')


print(index)

# Output: 1
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

## 10) `range` Function

The range() function in Python is a built-in function used to generate a sequence of numbers. It is often used in for loops to iterate over a sequence of numbers.

The basic syntax of the range() function is as follows: range(start_val, stop_val, step)

    start (optional): The starting value of the sequence. If omitted, it defaults to 0.  
    stop: The end value of the sequence (exclusive). The range() function generates numbers up to, but not including, this value.  
    step (optional): The step or the difference between each number in the sequence. If omitted, it defaults to 1.  

```python
for i in range(1, 10, 2):
    print(i)
# output: 1
#         3
#         5
#         7
#         9

```

## 11) `map()` Function

The `map()` function applies a given function to each element of an iterable (list, tuple etc.) and returns an iterator containing the results.

apply square() to each item of the numbers list:  
squared_numbers_iterator = map(square, numbers)

map(str, digits): Converts each digit in the list to a string.

## 12) `int()` function
Python int() function returns an integer from a given object or converts a number in a given base to a decimal.

int('0b110', 2): convert binary string to its decimal equivalent.(input should be string!!)




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


## 1370) Increasing Decreasing String

You are given a string s. Reorder the string using the following algorithm:

Pick the smallest character from s and append it to the result.  
Pick the smallest character from s which is greater than the last appended character to the result and append it.  
Repeat step 2 until you cannot pick more characters.  
Pick the largest character from s and append it to the result.  
Pick the largest character from s which is smaller than the last appended character to the result and append it.  
Repeat step 5 until you cannot pick more characters.  
Repeat the steps from 1 to 6 until you pick all characters from s.  
In each step, If the smallest or the largest character appears more than once you can choose any occurrence and append it to the result.  

Return the result string after sorting s with this algorithm.

Example 1:

Input: s = "aaaabbbbcccc"  
Output: "abccbaabccba"  
Explanation: After steps 1, 2 and 3 of the first iteration, result = "abc"  
After steps 4, 5 and 6 of the first iteration, result = "abccba"  
First iteration is done. Now s = "aabbcc" and we go back to step 1  
After steps 1, 2 and 3 of the second iteration, result = "abccbaabc"  
After steps 4, 5 and 6 of the second iteration, result = "abccbaabccba"  

Example 2:

Input: s = "rat"  
Output: "art"  
Explanation: The word "rat" becomes "art" after re-ordering it with the mentioned algorithm.  

```python
class Solution:
    def sortString(self, s: str) -> str:
        result = ""
        counts = {}
        letters = sorted(set(s))
        letters = list(letters)
        for char in s:
            counts[char] = s.count(char)
        
        while len(result)<len(s):
            for l in letters:
                if counts[l] > 0:
                    result += l
                    counts[l] -= 1
            
            for l in letters[::-1]:
                if counts[l] > 0:
                    result += l
                    counts[l] -= 1
            

        return result
```


## 66) Plus one

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

 

Example 1:

Input: digits = [1,2,3]  
Output: [1,2,4]  
Explanation: The array represents the integer 123.  
Incrementing by one gives 123 + 1 = 124.  
Thus, the result should be [1,2,4].  

Example 2:

Input: digits = [4,3,2,1]  
Output: [4,3,2,2]  
Explanation: The array represents the integer 4321.  
Incrementing by one gives 4321 + 1 = 4322.  
Thus, the result should be [4,3,2,2].  

Example 3:

Input: digits = [9]  
Output: [1,0]  
Explanation: The array represents the integer 9.  
Incrementing by one gives 9 + 1 = 10.  
Thus, the result should be [1,0].  
            
```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        # Convert the list of digits to an integer
        num = int("".join(map(str, digits)))
        
        # Increment the integer by 1
        num += 1
        
        # Convert the updated integer back to a list of digits
        result = [int(digit) for digit in str(num)]
        
        return result
```
## 14) Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:

Input: strs = ["flower","flow","flight"]  
Output: "fl"  

Example 2:

Input: strs = ["dog","racecar","car"]  
Output: ""  
Explanation: There is no common prefix among the input strings.  

Solution : https://medium.com/@d_dchris/10-methods-to-solve-the-longest-common-prefix-problem-using-python-leetcode-14-a87bb3eb0f3a







