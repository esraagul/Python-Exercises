# NOTES 
Python has the following data types built-in by default, in these categories:

Text Type:	str
Numeric Types:	int, float, complex
Sequence Types:	list, tuple, range
Mapping Type:	dict
Set Types:	            set, frozenset
Boolean Type:	bool
Binary Types:	bytes, bytearray, memoryview
None Type:	            NoneType

Difference between array and list: array can store elements only of the same type but list can store elements of different types.
list = ['esra', 28]
array = [22, 28]
********************************************************************************************************************************************************************


Empty array []
Empty array with zeros []*n

* init with values (can contain mixed types)
arr = [1, "eels"]

* get item by index (can be negative to access end of array)
arr = [1, 2, 3, 4, 5, 6]
arr[0]  # 1
arr[-1] # 6

* get length
length = len(arr)

* supports append and insert
arr.append(8)
arr.insert(6, 7)

********************************************************************************************************************************************************************
## 1) Dictionaries
Dictionary is a collection which is ordered and changeable. No duplicate members.
romans = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000 }
romans['I'] == 1
You can add key: value to the existing dictionary. i.e., romans['E'] = 100000
romans.keys() : will return a view object. The view object contains the keys of the dictionary, as a list.(does not take any parameters)
romans.values() : will return a view object that displays a list of all values in a given dictionary.(does not take any parameters)


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
********************************************************************************************************************************************************************

## 2) Stack of characters
A stack is a linear data structure that stores items in a Last-In/First-Out manner. (ust uste dizilmis kitaplar)
stack = []
stack.append('a') : adds a at the top of the stack
stack.append('b')
stack.append('c')
* out stack is cba from top to bottom
stack.pop() --> pops out the item at the top of the stack, that is c here.
********************************************************************************************************************************************************************

## 3) Strings

string.count()
txt = "I love apples, apple are my favorite fruit"
x = txt.count("apple")
print(x) ---> 2


## 4) Bin function

The bin() function returns the binary version of a specified integer. The result will always start with the prefix 0b.
bin(36) ---> 0b100100
x = bin(36)
x = x[2::] ---> 100100 (take the part starting with 2nd element including that element)


## 5) List
Lists are used to store multiple items in a single variable.


## 6) Set
Sets in Python are unordered collections of unique elements. 
By their nature, duplicates aren't allowed. Therefore, converting a list into a set removes the duplicates.
Sets do not have append function, instead set.add(element) is used.

## 7) Reversing an array
one way is to use reversed():
array = [1, 2, 3, 4, 5]
reversed_array = list(reversed(array))
print(reversed_array)  

or build-in function reverse():
array = [1, 2, 3, 4, 5]
array.reverse()
print(array)  

## 8) Sorted Function

sorted(arr, key=lambda x: (bin(x).count('1'), x)): 
The sorted function takes the input list arr and sorts its elements based on the key provided by the lambda function. Each element x in arr is transformed using the lambda function to obtain a tuple (bin(x).count('1'), x). The sorting is done based on these tuples, first by the count of '1' bits and then by the actual values of x.

********************************************************************************************************************************************************************

# QUESTIONS 

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



