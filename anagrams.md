An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase using all the original letters exactly once. 
For example, "dacb" is an anagram of "abdc".

**SORTED** 

a = ("h", "h", "a", "c", "f", "d", "e", "g")
x = sorted(a) ---> ['a', 'c', 'd', 'e', 'f', 'g', 'h', 'h']
x = sorted(a, reverse=True) ---> ['h', 'h', 'g', 'f', 'e', 'd', 'c', 'a']



*
2273. Find resultant array after removing anagrams
You are given a 0-indexed string array words, where words[i] consists of lowercase English letters.
In one operation, select any index i such that 0 < i < words.length and words[i - 1] and words[i] are anagrams, and delete words[i] from words. 
Keep performing this operation as long as you can select an index that satisfies the conditions.
Return words after performing all operations. It can be shown that selecting the indices for each operation in any arbitrary order will lead to the same result.

Input: words = ["abba","baba","bbaa","cd","cd"]
Output: ["abba","cd"]

Input: words = ["a","b","c","d","e"]
Output: ["a","b","c","d","e"]

``` python
class Solution:
    def removeAnagrams(self, words: List[str]) -> List[str]:
        i = 1
        while i<len(words):
            sort_word1 = sorted(words[i-1])
            sort_word2 = sorted(words[i])
            if sort_word1 == sort_word2:
                words.pop(i)
            else: 
                i += 1
            
                
        
        return words
```
