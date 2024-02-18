## Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target. You may assume that each input would have exactly one solution, and you may not use the same element twice. You can return the answer in any order.

Example 1: 
Input: nums = [2,7,11,15], target = 9  
Output: [0,1]  
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].   

Example 2: 
Input: nums = [3,2,4], target = 6  
Output: [1,2]  

Example 3: 
Input: nums = [3,3], target = 6  
Output: [0,1]  

**One-pass Hash Table**:
```python3
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dictionary = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in dictionary:
                return [i, dictionary[complement]]
            dictionary[nums[i]] = i
```

## Two Sum II-input array is sorted

Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length. Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2. The tests are generated such that there is exactly one solution. You may not use the same element twice. Your solution must use only constant extra space.

Example 1:

Input: numbers = [2,7,11,15], target = 9  
Output: [1,2]    
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].  

Example 2:
Input: numbers = [2,3,4], target = 6  
Output: [1,3]  
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

Example 3:  
Input: numbers = [-1,0], target = -1  
Output: [1,2]  
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].  

**Two Pointers**
```python3
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left = 0
        right = len(numbers)-1
        while left<right:
            curr_sum = numbers[left]+numbers[right]
            if curr_sum == target:
                return [left+1, right+1]
            elif curr_sum>target:
                right-=1
            else:
                left+=1
                
        return []
        
```

## 3Sum

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.


Example 1:

Input: nums = [-1,0,1,2,-1,-4]  
Output: [[-1,-1,2],[-1,0,1]]  
Explanation:   
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.  
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.  
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.  
The distinct triplets are [-1,0,1] and [-1,-1,2].  
Notice that the order of the output and the order of the triplets does not matter.  
Example 2:

Input: nums = [0,1,1]  
Output: []  
Explanation: The only possible triplet does not sum up to 0.  
Example 3:

Input: nums = [0,0,0]  
Output: [[0,0,0]]  
Explanation: The only possible triplet sums up to 0.  

**Two Pointers**
```python3
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        for index, val in enumerate(nums):
            if index>0 and val==nums[index-1]:
                continue
            l = index + 1
            r = len(nums)-1
            while l<r:
                threeSum = val+nums[l]+nums[r]
                if threeSum>0:
                    r-=1
                elif threeSum<0:
                    l+=1
                else:
                    res.append([val, nums[l], nums[r]])
                    l+=1
                    while l<r and nums[l]==nums[l-1]:
                        l+=1
        return res
                
        
```

observe that the iteration in the else part is necessary because there might be other solutions with the same element. 

For example,  
nums = [-1,0,1,2,-1,-4] then the answer is [[-1,-1,2],[-1,0,1]].
