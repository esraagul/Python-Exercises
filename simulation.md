## 1560. Most Visited Sector in Circular Track

Given an integer n and an integer array rounds. We have a circular track which consists of n sectors labeled from 1 to n. A marathon will be held on this track, the marathon consists of m rounds. The ith round starts at sector rounds[i - 1] and ends at sector rounds[i]. For example, round 1 starts at sector rounds[0] and ends at sector rounds[1]

Return an array of the most visited sectors sorted in ascending order.

Notice that you circulate the track in ascending order of sector numbers in the counter-clockwise direction (See the first example).


Input: n = 4, rounds = [1,3,1,2]  
Output: [1,2]   
Explanation: The marathon starts at sector 1. The order of the visited sectors is as follows:  
1 --> 2 --> 3 (end of round 1) --> 4 --> 1 (end of round 2) --> 2 (end of round 3 and the marathon)  
We can see that both sectors 1 and 2 are visited twice and they are the most visited sectors. Sectors 3 and 4 are visited only once.  
Example 2:

Input: n = 2, rounds = [2,1,2,1,2,1,2,1,2]  
Output: [2]  
Example 3:

Input: n = 7, rounds = [1,3,5,7]  
Output: [1,2,3,4,5,6,7]  


```python3
class Solution:
    def mostVisited(self, n: int, rounds: List[int]) -> List[int]:
        visits = [0]*n
        for i in range(len(rounds)-1):
            start = rounds[i]
            end = rounds[i+1]
            while start!=end:
                visits[start-1]+=1
                start = (start%n)+1
            
        visits[rounds[-1]-1] += 1
        max_visit = max(visits)
        most_visited = [i+1 for i,val in enumerate(visits) if val==max_visit]

        return most_visited
```

Explanation: The code simulates the marathon by iterating through the given rounds and updating the visit counts for each sector accordingly. This approach is effective for small to moderate values of n and the length of the rounds array.

In a simulation approach, you are essentially mimicking the process or scenario to gather information or results. The code takes into account the circular nature of the track and updates the visit counts based on the specified rounds. It does not require any advanced mathematical or optimization techniques, making it suitable for a straightforward simulation.

The time complexity of the solution is O(m * n), where m is the length of the rounds array and n is the number of sectors. In the worst case, each sector may be visited in every round. If your input values are within a reasonable range, this simulation approach should work well. If you are dealing with very large inputs, you might need to explore more optimized algorithms.


## 867. Transpose Matrix


Given a 2D integer array matrix, return the transpose of matrix.

The transpose of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

Example 1:

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]  
Output: [[1,4,7],[2,5,8],[3,6,9]]  
Example 2:

Input: matrix = [[1,2,3],[4,5,6]]  
Output: [[1,4],[2,5],[3,6]]  

```python3
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        num_rows = len(matrix)
        num_cols = len(matrix[0])
        ans = [[0]*num_rows for _ in range(num_cols)]
        for r, row in enumerate(matrix):
            for c, val in enumerate(row):
                ans[c][r] = val
        return ans
```
