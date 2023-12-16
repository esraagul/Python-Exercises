2038. Remove colored pieces if both neighbors are the same color:
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
1529. Minimum Suffix Flips:
      
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



## 38. Count and Say
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
```

note: self.countAndSay(n - 1) is recursive way of calling the function

self: In Python, self is a reference to the instance of the class. When a method is called on an instance of a class, self is used to refer to that instance




## 3) Longest Substring Without Repeating Characters

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

My solution:
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

Sliding window technique:





