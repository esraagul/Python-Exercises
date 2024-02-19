## Depth First Search

Meaning vertical before horizontal.

### 733.Flood Fill

An image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image.

You are also given three integers sr, sc, and color. You should perform a flood fill on the image starting from the pixel image[sr][sc].

To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with color.

Return the modified image after performing the flood fill.


<img width="720" alt="Screen Shot 2024-02-19 at 2 48 09 PM" src="https://github.com/esraagul/Python-Exercises/assets/41425202/f9c73790-1752-427b-afd9-c4e62793b42e">




```python3
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:
        height = len(image)
        width = len(image[0])
        curr_color = image[sr][sc]
        def dfs(r,c):
            if 0<=r<height and 0<=c<width and image[r][c]==curr_color and image[r][c]!=color:
                image[r][c] = color
                dfs(r+1,c)
                dfs(r-1,c)
                dfs(r,c+1)
                dfs(r,c-1)

        dfs(sr,sc)

        return image
```
