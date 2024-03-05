## Table of Contents
- [2038. Remove colored pieces if both neighbors are the same color](#2038)
- [1529. Minimum Suffix Flips](#1529)
- [38. Count and Say](#38)
- [3.Longest Substring Without Repeating Characters](#3)
- [56. Merge Intervals](#56)
- [2610. Convert an array into 2D array with conditions](#2610)
- [647. Palindromic Substring](#647)





### 2038. Remove colored pieces if both neighbors are the same color <a name="2038"></a>
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        a = 0
        b = 0
        for i in range(1,len(colors)-1):
            if colors[i-1]==colors[i]==colors[i+1]:
                if colors[i] == 'A':
                    a += 1
                else:
                    b += 1
            
        return a-b>=1
```
with zip:
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        a,b=0,0
        for i,ii,iii in zip(colors,colors[1:],colors[2:]):
            if 'A'==i==ii==iii:a+=1
            elif 'B'==i==ii==iii:b+=1
        return b<a
```
### 1529. Minimum Suffix Flips <a name="1529"></a>
      
You are given a 0-indexed binary string target of length n. You have another binary string s of length n that is initially set to all zeros. You want to make s equal to target.

In one operation, you can pick an index i where 0 <= i < n and flip all bits in the inclusive range [i, n - 1]. Flip means changing '0' to '1' and '1' to '0'.

Return the minimum number of operations needed to make s equal to target.


Example 1:

Input: target = "10111"
Output: 3
Explanation: Initially, s = "00000".
Choose index i = 2: "00000" -> "00111"
Choose index i = 0: "00111" -> "11000"
Choose index i = 1: "11000" -> "10111"
We need at least 3 flip operations to form target.
Example 2:

Input: target = "101"
Output: 3
Explanation: Initially, s = "000".
Choose index i = 0: "000" -> "111"
Choose index i = 1: "111" -> "100"
Choose index i = 2: "100" -> "101"
We need at least 3 flip operations to form target.
Example 3:

Input: target = "00000"
Output: 0
Explanation: We do not need any operations since the initial s already equals target.

Code with high time complexity:

```python
class Solution:
    def minFlips(self, target: str) -> int:
        s = "0"*len(target)
        counts = 0
        for i in range(len(target)):
            if target[i]!=s[i]:
                counts+=1
                s = s[:i]+''.join(['1' if bit=='0'else '0' for bit in s[i:]])
                # The empty string '' acts as a separator, indicating that there should be no characters between the elements when they are joined.
        return counts

```

instead of comparing entire strings and performing operations, the code iterates through the target string. For each bit in the target, it compares it with the current bit. If they are different, it performs a flip operation by toggling the current bit. This approach avoids unnecessary string operations and should be more efficient.

```python
def minFlips(target):
    operations = 0
    current_bit = '0'  # Initialize the current bit as '0'
    
    for bit in target:
        # If the current bit of target is different from current bit
        if bit != current_bit:
            operations += 1
            # Flip the current bit
            current_bit = '1' if current_bit == '0' else '0'
    
    return operations
```



### 38. Count and Say <a name="38"></a>
The count-and-say sequence is a sequence of digit strings defined by the recursive formula:

countAndSay(1) = "1"  
countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.
To determine how you "say" a digit string, split it into the minimal number of substrings such that each substring contains exactly one unique digit. Then for each substring, say the number of digits, then say the digit. Finally, concatenate every said digit.

For example, the saying and conversion for digit string "3322251":

------> two 3's, three 2's, one 5, and one 1 : 23321511

Given a positive integer n, return the nth term of the count-and-say sequence.

Example 1:

Input: n = 1  
Output: "1"  
Explanation: This is the base case.  

Example 2:

Input: n = 4  
Output: "1211"  
Explanation:  
countAndSay(1) = "1"  
countAndSay(2) = say "1" = one 1 = "11"  
countAndSay(3) = say "11" = two 1's = "21"  
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"  

Hint 1:

Create a helper function that maps an integer to pairs of its digits and their frequencies. For example, if you call this function with "223314444411", then it maps it to an array of pairs [[2,2], [3,2], [1,1], [4,5], [1, 2]].

Hint 2:

Create another helper function that takes the array of pairs and creates a new integer. For example, if you call this function with [[2,2], [3,2], [1,1], [4,5], [1, 2]], it should create "22"+"23"+"11"+"54"+"21" = "2223115421".

Hint 3:

Now, with the two helper functions, you can start with "1" and call the two functions alternatively n-1 times. The answer is the last integer you will obtain.


```python
class Solution:
    def countAndSay(self, n: int) -> str:
        def digits_freq(number):  # Helper function to get digit frequencies
            digit_freq = []
            count = 0
            i = 0
            while i < len(number):
                count = 1
                while i + 1 < len(number) and number[i + 1] == number[i]:
                    count += 1
                    i += 1
                digit_freq.append([number[i], count])
                i += 1
            return digit_freq

        def pairs_to_string(array):  # Helper function to concatenate pairs
            result = ''
            for a in array:
                result += str(a[1]) + str(a[0])
            return result

        if n == 1:
            return '1'
        else:
            # Recursively call countAndSay for the previous level (n-1)
            prev_result = self.countAndSay(n - 1)
            
            # Get digit frequencies for the previous result
            digit_freq = digits_freq(prev_result)
            
            # Convert digit frequencies to string
            result = pairs_to_string(digit_freq)
            
            return result


### Another way of writing digits_freq function:
def digits_freq(number):
            digit_freq = []
            count = 1
            for i in range(1, len(number)):
                if number[i]==number[i-1]:
                    count+=1
                else:
                    digit_freq.append([number[i-1], count])
                    count = 1
            digit_freq.append([number[-1], count])  # Handle the last digit
            return digit_freq
```

note: self.countAndSay(n - 1) is recursive way of calling the function

self: In Python, self is a reference to the instance of the class. When a method is called on an instance of a class, self is used to refer to that instance




### 3. Longest Substring Without Repeating Characters <a name="3"></a>

Given a string s, find the length of the longest substring without repeating characters.


Example 1:

Input: s = "abcabcbb"  
Output: 3  
Explanation: The answer is "abc", with the length of 3.  

Example 2:

Input: s = "bbbbb"  
Output: 1  
Explanation: The answer is "b", with the length of 1.  

Example 3:

Input: s = "pwwkew"  
Output: 3  
Explanation: The answer is "wke", with the length of 3.  
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.  

My solution: O(n)
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        ans = []
        max_length = 0

        for i in s:
            if i not in ans:
                ans.append(i)
                max_length = max(max_length, len(ans))
            else:
                ans = ans[ans.index(i) + 1:] + [i]

        return max_length
```

Sliding window technique: O(n)

A sliding window is an abstract concept commonly used in array/string problems. A window is a range of elements in the array/string which usually defined by the start and end indices, i.e. [i,j)[i, j)[i,j) (left-closed, right-open). A sliding window is a window "slides" its two boundaries to the certain direction. For example, if we slide [i,j)[i, j)[i,j) to the right by 111 element, then it becomes [i+1,j+1)[i+1, j+1)[i+1,j+1) (left-closed, right-open).   

Intuition

Given a substring with a fixed end index in the string, maintain a HashMap(dictionary) to record the frequency of each character in the current substring. If any character occurs more than once, drop the leftmost characters until there are no duplicate characters.

```python
from collections import Counter
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        chars = Counter()

        left = right = 0

        res = 0
        while right < len(s):
            r = s[right]
            chars[r] += 1

            while chars[r] > 1:
                l = s[left]
                chars[l] -= 1
                left += 1

            res = max(res, right - left + 1)

            right += 1
        return res

```

Sliding Window Optimized : O(n)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        ans = 0
        # mp stores the current index of a character
        mp = {}

        i = 0
        # try to extend the range [i, j]
        for j in range(n):
            if s[j] in mp:
                i = max(mp[s[j]], i)

            ans = max(ans, j - i + 1)
            mp[s[j]] = j + 1

        return ans
```

Intuition

The above solution requires at most 2n steps. In fact, it could be optimized to require only n steps. Instead of using a set to tell if a character exists or not, we could define a mapping of the characters to its index. Then we can skip the characters immediately when we found a repeated character.


i = 0: Initialize a variable i to represent the start of the current substring.  
Iterate over the string using a sliding window approach with the right pointer j.  
Check if the character at index j (s[j]) is already in the mp dictionary.  
If it is, update the start pointer i to the maximum of the current index of the character in mp and the current value of i.  
Update the length of the current substring (ans) by taking the maximum of its current value and the length of the current window (j - i + 1).  
Update the current index of the character in mp to j + 1 (the next index).  



### 56. Merge Intervals <a name="56"></a>
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]  
Output: [[1,6],[8,10],[15,18]]  
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].  
Example 2:

Input: intervals = [[1,4],[4,5]]  
Output: [[1,5]]  
Explanation: Intervals [1,4] and [4,5] are considered overlapping.  

```python3
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda x: x[0])
        ans = []
        for interval in intervals:
            if not ans or ans[-1][1]<interval[0]:
                ans.append(interval)
            else:
                ans[-1][1] = max(ans[-1][1], interval[1])
        return ans
```

Another way without checking if answer is empty, just add first element to the result list:
```python3
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda x: x[0])
        result = [intervals[0]]
        for i in range(1, len(intervals)):
            if intervals[i][0]<=result[-1][1]:
                result[-1][1] = max(intervals[i][1], result[-1][1])
            else:
                result.append(intervals[i])

        return result
```
 
### 2610. Convert an array into 2D array with conditions <a name="2610"></a>

You are given an integer array nums. You need to create a 2D array from nums satisfying the following conditions:

The 2D array should contain only the elements of the array nums.
Each row in the 2D array contains distinct integers.
The number of rows in the 2D array should be minimal.
Return the resulting array. If there are multiple answers, return any of them.

Note that the 2D array can have a different number of elements on each row.

 

Example 1:

Input: nums = [1,3,4,1,2,3,1]  
Output: [[1,3,4,2],[1,3],[1]]  
Explanation: We can create a 2D array that contains the following rows:  
- 1,3,4,2  
- 1,3  
- 1  
All elements of nums were used, and each row of the 2D array contains distinct integers, so it is a valid answer.
It can be shown that we cannot have less than 3 rows in a valid array.
Example 2:

Input: nums = [1,2,3,4]  
Output: [[4,3,2,1]]  
Explanation: All elements of the array are distinct, so we can keep all of them in the first row of the 2D array.   


```python3
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        # Initialize an empty list to store the result
        ans = []

        # Iterate through each element in the input list 'nums'
        for num in nums:
            # Flag to keep track of whether the current 'num' is added to any existing row
            added = False

            # Iterate through existing rows in 'ans'
            for row in ans:
                # Check if the current 'num' is not already present in the current 'row'
                if num not in row:
                    # If 'num' is not in 'row', append 'num' to 'row'
                    row.append(num)
                    # Set 'added' to True to indicate that 'num' has been added
                    added = True
                    # Break out of the inner loop since 'num' has been added to a row
                    break

            # Check if 'added' is still False after iterating through all rows
            if not added:
                # If 'added' is False, create a new row containing only the current 'num'
                ans.append([num])

        # Return the final result
        return ans
```

### 647. Palindromic Substring <a name="647"></a>

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

 

Example 1:

Input: s = "abc"  
Output: 3  
Explanation: Three palindromic strings: "a", "b", "c".  
Example 2:

Input: s = "aaa"  
Output: 6  
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".  


```python3
class Solution:
    def countSubstrings(self, s: str) -> int:
        count = 0
        # odd length palindromes: char is in the middle, expand left and right.
        for i in range(len(s)):
            r = l = i
            while l>=0 and r<len(s) and s[l]==s[r]:
                count += 1
                l -= 1
                r += 1
        # even length palindromes: counting aa and aa in aaab, right pointer is i+1.
        for i in range(len(s)):
            l = i
            r = i+1
            while l>=0 and r<len(s) and s[l]==s[r]:
                count += 1
                l -= 1
                r += 1
        return count
```
        





