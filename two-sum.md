## Table of Contents
1. [Two Sum](#two-sum)
2. [Two Sum II - Input Array is Sorted](#two-sum-ii-input-array-is-sorted)
3. [3Sum](#3sum)
4. [3Sum Smaller](#3sum-smaller)
5. [3Sum Closest](#3sum-closest)

## Two Sum <a name="two-sum"></a>

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

## Two Sum II - Input Array is Sorted <a name="two-sum-ii-input-array-is-sorted"></a>

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

## 3Sum <a name="3sum"></a>

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

**use TwoSumII as separate function:**
```python3
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        for i in range(len(nums)):
            if nums[i]>0:
                break
            if i==0 or nums[i]!=nums[i-1]:
                self.twoSumII(nums,i,res)
        return res

    def twoSumII(self, nums: List[int], i: int, res: List[List[int]]):
        l = i+1
        r = len(nums)-1
        while l<r:
            sum = nums[i]+nums[l]+nums[r]
            if sum>0:
                r-=1
            elif sum<0:
                l+=1
            else:
                res.append([nums[i], nums[l], nums[r]])
                l+=1
                while l<r and nums[l]==nums[l-1]:
                    l+=1
```


**without using sorting:**
```python3
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = set()
        dups = set()
        seen = {}
        for index1, val1 in enumerate(nums):
            if val1 not in dups:
                dups.add(val1)
                for index2, val2 in enumerate(nums[index1+1:]):
                    complement = -val1-val2
                    if complement in seen and seen[complement]==index1:
                        res.add(tuple(sorted((val1,val2,complement))))  #set() takes tuples(i.e.()). tuple converts sorted(tuple) into tuple.
                    seen[val2] = index1  # This ensures that val2 is associated with the last index of the outer loop when it is encountered in the inner loop.
        return res


## 3Sum Smaller <a name="3sum-smaller"></a>

Given an array of n integers nums and an integer target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target.

Example 1:

Input: nums = [-2,0,1,3], target = 2  
Output: 2  
Explanation: Because there are two triplets which sums are less than 2:  
[-2,0,1]   
[-2,0,3]  
Example 2:  

Input: nums = [], target = 0  
Output: 0  
Example 3:  

Input: nums = [0], target = 0  
Output: 0

example: nums=[3,1,0,-2], target=4
output: 3

```python3
class Solution:
    def threeSumSmaller(self, nums: List[int], target: int) -> int:
        counter = 0
        nums.sort()
        for index, val in enumerate(nums):
            l = index+1
            r = len(nums)-1
            while l<r:
                threeSum = val+nums[l]+nums[r]
                if threeSum<target:
                    counter+=r-l # All pairs (nums[index], nums[l], nums[k]) are valid for l < k < r
                    l+=1
                else:
                    r-=1
        return counter

```

## 3Sum Closest <a name="3sum-closest"></a>

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

 

Example 1:

Input: nums = [-1,2,1,-4], target = 1  
Output: 2  
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).  
Example 2:

Input: nums = [0,0,0], target = 1  
Output: 0   
Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).  

**Two pointers:**

```python3
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        closest_sum = float('inf') # set it to positive infinity
        for index, val in enumerate(nums):
            l = index+1
            r = len(nums)-1
            while l<r:
                curr_sum = val + nums[l] + nums[r]
                if abs(curr_sum-target)<abs(closest_sum-target):
                    closest_sum = curr_sum
                
                if curr_sum<target:
                    l+=1
                elif curr_sum>target:
                    r-=1
                else:
                    return closest_sum
        return closest_sum
```




